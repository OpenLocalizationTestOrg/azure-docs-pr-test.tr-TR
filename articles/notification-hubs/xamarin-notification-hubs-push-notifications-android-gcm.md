---
title: "aaaGet Xamarin.Android uygulamaları için Notification Hubs ile çalışmaya | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Xamarin Android uygulaması öğrenin."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="0b7a6-103">Android için Xamarin ile Notification Hubs'ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0b7a6-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0b7a6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0b7a6-104">Overview</span></span>
<span data-ttu-id="0b7a6-105">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooa Xamarin.Android uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="0b7a6-106">Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan boş bir Xamarin.Android uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="0b7a6-107">Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="0b7a6-108">Merhaba tamamlanmış kod hello kullanılabilir [NotificationHubs uygulaması] [ GitHub] örnek.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="0b7a6-109">Bu öğretici Notification Hubs kullanımında hello basit yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0b7a6-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="0b7a6-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="0b7a6-111">Bu öğreticinin hello tamamlanan kodu Github'da bulunabilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="0b7a6-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b7a6-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0b7a6-112">Prerequisites</span></span>
<span data-ttu-id="0b7a6-113">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="0b7a6-114">Windows'ta Xamarin ile Visual Studio veya Mac OS X'te Xamarin Studio. Tam yükleme yönergeleri [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="0b7a6-115">Etkin Google hesabı</span><span class="sxs-lookup"><span data-stu-id="0b7a6-115">Active Google account</span></span>
* <span data-ttu-id="0b7a6-116">[Azure Mesajlaşma Bileşeni]</span><span class="sxs-lookup"><span data-stu-id="0b7a6-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="0b7a6-117">[Google Cloud Messaging İstemci Bileşeni]</span><span class="sxs-lookup"><span data-stu-id="0b7a6-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="0b7a6-118">Bu öğreticiyi tamamlamak Xamarin.Android uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b7a6-119">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="0b7a6-120">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0b7a6-121">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="0b7a6-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="0b7a6-122">Google Cloud Messaging'i etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0b7a6-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="0b7a6-123">Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0b7a6-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="0b7a6-124">Merhaba tıklatın <b>yapılandırma</b> sekmesinde hello üstünde, hello girin <b>API anahtarı</b> değerini hello önceki bölümde edindiğiniz ve ardından <b>kaydetmek</b>.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="0b7a6-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="0b7a6-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="0b7a6-126">Bildirim hub'ınız şimdi GCM ile yapılandırılmış toowork olduğu ve toosend anında iletme bildirimleri ve uygulama tooreceive bildirimleri kaydetmek hello bağlantı dizeleri tooboth sahip.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="0b7a6-127">Uygulama toohello bildirim hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="0b7a6-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="0b7a6-128">Yeni bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b7a6-128">Create a new project</span></span>
1. <span data-ttu-id="0b7a6-129">Xamarin Studio'da **New Solution**'a (Yeni Çözüm), **Android App** 'e (Android Uygulaması) ve **Next**'e (İleri) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="0b7a6-130">**App Name**'i (Uygulama Adı) ve **Identifier**'ı (Tanımlayıcı) girin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="0b7a6-131">Merhaba tıklatın **Target Plaforms** toosupport istediğiniz ve ardından **sonraki** ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="0b7a6-132">Bu, yeni bir Android projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="0b7a6-133">Merhaba çözüm görünümü yeni projenize sağ tıklayıp seçerek hello proje özelliklerini açın **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="0b7a6-134">Select hello **Android uygulaması** hello öğesinde **yapı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="0b7a6-135">Bu hello ilk harfini emin olun, **paket adı** küçük harf.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0b7a6-136">Merhaba hello paket adının ilk harfi küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="0b7a6-137">Aksi durumda, aşağıdaki anında iletme bildirimleri için **BroadcastReceiver** ve **IntentFilter** öğelerinizi kaydettiğinizde uygulama bildirim hataları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="0b7a6-138">İsteğe bağlı olarak, kümesi hello **Minimum Android sürümü** tooanother API düzeyi.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="0b7a6-139">İsteğe bağlı olarak, kümesi hello **hedef Android sürümü** toohello (olmalıdır API düzeyi 8 veya sonraki sürümler) tootarget istediğiniz başka bir API sürümü.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="0b7a6-140">Tıklatın **Tamam** ve Kapat hello proje Seçenekleri iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="0b7a6-141">Merhaba gerekli bileşenleri tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="0b7a6-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="0b7a6-142">Hello Google Cloud Messaging istemcisi Xamarin bileşen Deposu'nda hello üzerinde kullanılabilir hello Xamarin.Android içinde anında iletme bildirimlerini destekleme işlemini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="0b7a6-143">Xamarin.Android uygulaması Hello bileşenleri klasörü sağ tıklatın ve seçin **daha almak bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="0b7a6-144">Merhaba Ara **Azure Mesajlaşma** bileşeni ve toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="0b7a6-145">Merhaba Ara **Google Cloud Messaging istemcisi** bileşeni ve toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="0b7a6-146">Projenizdeki bildirim hub'larını ayarlama</span><span class="sxs-lookup"><span data-stu-id="0b7a6-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="0b7a6-147">Android uygulamanız ve bildirim hub'ınız için bilgisinden hello toplayın:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="0b7a6-148">**GoogleProjectNumber**: hello hello Google Developer Portal'daki uygulamanıza genel bakış'nden bu proje numarası değerini alın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="0b7a6-149">Merhaba portalında hello uygulama oluştururken bu değeri daha önce Not yaptığınız.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="0b7a6-150">**Dinleme bağlantı dizesi**: hello hello Panoda [Klasik Azure portalı], tıklatın **bağlantı dizelerini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="0b7a6-151">Kopya hello *DefaultListenSharedAccessSignature* bu değer için bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="0b7a6-152">**Hub adı**: Bu hello Merhaba, hub'dan adıdır [Klasik Azure portalı].</span><span class="sxs-lookup"><span data-stu-id="0b7a6-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="0b7a6-153">Örneğin, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="0b7a6-154">Oluşturma bir **Constants.cs** Xamarin projeniz için sınıf ve sabit değerleri hello sınıfında aşağıdaki hello tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="0b7a6-155">Merhaba yer tutucuları değerleriniz ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="0b7a6-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="0b7a6-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="0b7a6-157">}</span><span class="sxs-lookup"><span data-stu-id="0b7a6-157">}</span></span>
2. <span data-ttu-id="0b7a6-158">Merhaba aşağıdaki using deyimlerini çok**MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="0b7a6-159">Bir örnek değişkeni toohello ekleme `MainActivity` hello uygulama çalışırken, kullanılan tooshow uyarı iletişim kutusu sınıfı:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="0b7a6-160">Merhaba yönteminde aşağıdaki hello oluşturma **MainActivity** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="0b7a6-161">Merhaba, `OnCreate` yöntemi **MainActivity.cs**, hello başlatma `instance` değişkeni ve çok bir çağrı ekleyin`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="0b7a6-162">**MyBroadcastReceiver** adlı yeni bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0b7a6-163">Aşağıda, sıfırdan bir **BroadcastReceiver** sınıfı oluşturma konusunda size yol göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="0b7a6-164">Ancak, hızlı alternatif toomanually oluşturma **MyBroadcastReceiver.cs** toorefer toohello olan **GcmService.cs** helloiledahilhelloörnekXamarin.Androidprojesindebulunandosya[NotificationHubs örnekleri][GitHub].</span><span class="sxs-lookup"><span data-stu-id="0b7a6-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="0b7a6-165">Çoğaltma **GcmService.cs** ve sınıf adlarını değiştirmek de harika yer toostart olabilir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="0b7a6-166">Merhaba aşağıdaki using deyimlerini çok**MyBroadcastReceiver.cs** (toohello bileşeni ve daha önce eklediğimiz derleme başvuran):</span><span class="sxs-lookup"><span data-stu-id="0b7a6-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="0b7a6-167">İçinde **MyBroadcastReceiver.cs**, izin istekleri arasında hello aşağıdaki hello eklemek **kullanarak** deyimleri ve hello **ad alanı** bildirimi:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="0b7a6-168">İçinde **MyBroadcastReceiver.cs**, hello değiştirme **MyBroadcastReceiver** sınıf toomatch hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="0b7a6-169">**MyBroadcastReceiver.cs**'ye **GcmServiceBase**'den türetilen **PushHandlerService** adlı başka bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="0b7a6-170">Tooapply hello emin olun **hizmet** özniteliği toohello sınıfı:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="0b7a6-171">**GcmServiceBase**; **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** ve **OnError()** yöntemlerini uygular.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="0b7a6-172">Bizim **PushHandlerService** uygulama sınıfımızın bu yöntemleri geçersiz kılması gerekir ve bu yöntemleri hello bildirim hub'ı ile yanıt toointeracting ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="0b7a6-173">Merhaba geçersiz kılma **OnRegistered()** yönteminde **PushHandlerService** koddan hello kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="0b7a6-174">Merhaba, **OnRegistered()** Yukarıdaki kod, belirli Mesajlaşma kanallarına için hello özelliği toospecify etiketleri tooregister unutmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="0b7a6-175">Merhaba geçersiz kılma **Onmessageoptions** yönteminde **PushHandlerService** koddan hello kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="0b7a6-176">Merhaba aşağıdakileri ekleyin **Pushhandlerservice** ve **Createnotification** yöntemleri çok**PushHandlerService** bir bildirim alındığında kullanıcıları bilgilendirmek için.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0b7a6-177">Android sürüm 5.0 ve sonrasındaki bildirim tasarımı önceki sürümlerden önemli ölçüde farklıdır.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="0b7a6-178">Bunu Android 5.0 veya sonraki sürümlerinde test ederseniz hello uygulama tooreceive hello bildirim çalıştıran toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="0b7a6-179">Daha fazla bilgi için bkz. [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Android Bildirimleri).</span><span class="sxs-lookup"><span data-stu-id="0b7a6-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="0b7a6-180">**OnUnRegistered()**, **OnRecoverableError()** ve **OnError()** soyut üyelerini geçersiz kılarak kodunuzu derleyin:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="0b7a6-181">Merhaba öykünücüsünde uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0b7a6-181">Run your app in hello emulator</span></span>
<span data-ttu-id="0b7a6-182">Bu uygulamayı hello öykünücüde çalıştırırsanız, bir Android sanal cihazı (Google API'lerini destekleyen AVD) kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b7a6-183">Sipariş tooreceive anında iletme bildirimlerini Android sanal Cihazınızda bir Google hesabı ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="0b7a6-184">(Merhaba öykünücüsünde çok gidin**ayarları** tıklatıp **hesabı Ekle**.) Ayrıca, bu hello öykünücüsü bağlı toohello Internet olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="0b7a6-185">Android sürüm 5.0 ve sonrasındaki bildirim tasarımı önceki sürümlerden önemli ölçüde farklıdır.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="0b7a6-186">Daha fazla bilgi için bkz. [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Android Bildirimleri).</span><span class="sxs-lookup"><span data-stu-id="0b7a6-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="0b7a6-187">**Tools**'da (Araçlar), **Open Android Emulator Manager** (Android Öykünücüsü Yöneticisini Aç) seçeneğine tıklayın, cihazınızı açın ve ardından **Edit** (Düzenle) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="0b7a6-188">**Target** (Hedef) içinde **Google APIs** (Google API'leri) seçeneğini belirleyin ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="0b7a6-189">Merhaba üst araç çubuğunda tıklatın **çalıştırmak**ve ardından uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="0b7a6-190">Bu hello öykünücüyü başlatır ve hello uygulama çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="0b7a6-191">Merhaba uygulama alır hello *RegistrationId* GCM ve hello bildirim hub'ına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="0b7a6-192">Arka ucunuzdan bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="0b7a6-192">Send notifications from your backend</span></span>
<span data-ttu-id="0b7a6-193">Hello bildirimleri göndererek uygulamanızda bildirim almayı test edebilirsiniz [Klasik Azure portalı] ekranda hello aşağıda gösterildiği gibi hello bildirim hub'ındaki sekmesi hello hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="0b7a6-194">Anında iletme bildirimleri normalde, uyumlu bir kitaplık aracılığıyla Mobile Services veya ASP.NET gibi bir arka uç hizmetinde gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="0b7a6-195">Bir kitaplık arka ucunuz için kullanılabilir değilse, toosend bildirim iletilerini doğrudan hello REST API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="0b7a6-196">Bildirimleri göndermek için tooreview isteyebileceğiniz diğer bazı öğreticilerin bir listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="0b7a6-197">ASP.NET: Bkz [Notification Hubs kullanma toopush bildirimleri toousers].</span><span class="sxs-lookup"><span data-stu-id="0b7a6-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="0b7a6-198">Azure Notification Hubs Java SDK: bkz [nasıl toouse Java'dan Notification Hubs](notification-hubs-java-push-notification-tutorial.md) Java'dan bildirim göndermek için.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="0b7a6-199">Android geliştirmesi için Eclipse'te sınanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="0b7a6-200">PHP: Bkz [nasıl toouse php'den Notification Hubs](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0b7a6-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="0b7a6-201">Merhaba sonraki alt hello öğreticinin içinde bir .NET konsol uygulaması kullanarak ve bir node betiği aracılığıyla mobil hizmet kullanarak bildirim gönderin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="0b7a6-202">(İsteğe bağlı) .NET uygulaması kullanarak bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="0b7a6-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="0b7a6-203">Bu bölümde, .NET konsol uygulaması kullanarak bildirim göndereceğiz</span><span class="sxs-lookup"><span data-stu-id="0b7a6-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="0b7a6-204">Yeni bir Visual C# konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="0b7a6-205">Visual Studio'da **Araçlar**'a, **NuGet Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="0b7a6-206">Bu, Visual Studio'da Paket Yöneticisi konsolu hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="0b7a6-207">Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="0b7a6-208">Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="0b7a6-209">Merhaba Program.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="0b7a6-210">İçinde `Program` sınıfı, yöntem aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="0b7a6-211">Merhaba yer tutucu metnini güncelleştirin, *DefaultFullSharedAccessSignature* hello bağlantı dizenizi ve hub adı [Klasik Azure portalı].</span><span class="sxs-lookup"><span data-stu-id="0b7a6-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="0b7a6-212">Hello aşağıdaki satırları ekleyin, **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="0b7a6-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="0b7a6-213">Merhaba F5 anahtar toorun hello uygulama tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="0b7a6-214">Merhaba uygulamada bir bildirim almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="0b7a6-215">(İsteğe bağlı) Mobil hizmet kullanarak bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="0b7a6-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="0b7a6-216">[Mobile Services'i kullanmaya başlama]'yı izleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="0b7a6-217">İçinde toohello oturum [Klasik Azure portalı]ve mobil hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="0b7a6-218">Select hello **Zamanlayıcı** hello üst sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="0b7a6-219">Yeni bir zamanlanan iş oluşturun, ad ekleyin ve **İsteğe bağlı**'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="0b7a6-220">Merhaba iş oluşturulduğunda hello iş adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="0b7a6-221">Merhaba ardından **betik** hello üst çubuğu sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="0b7a6-222">Komut dosyası Zamanlayıcı işlevinizin içine aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="0b7a6-223">Bildirim hub'ı adı ve hello için bağlantı dizenizi emin tooreplace hello yer tutucularını olun *DefaultFullSharedAccessSignature* daha önce edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="0b7a6-224">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="0b7a6-225">Tıklatın **bir kez çalıştır** hello alt çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="0b7a6-226">Bir bildirim almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b7a6-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b7a6-227">Next steps</span></span>
<span data-ttu-id="0b7a6-228">Bu basit örnekte, Android cihazları bildirimleri tooall yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="0b7a6-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="0b7a6-229">Buna belirli kullanıcılara tootarget sipariş, toohello öğretici başvurun [Notification Hubs kullanma toopush bildirimleri toousers].</span><span class="sxs-lookup"><span data-stu-id="0b7a6-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="0b7a6-230">Toosegment kullanıcılarınızı ilgi alanı gruplarına göre isterseniz, okuyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend].</span><span class="sxs-lookup"><span data-stu-id="0b7a6-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="0b7a6-231">Hakkında daha fazla bilgi toouse bildirim hub'ları [Notification Hubs Kılavuzu] ve hello [bildirim hub'ları nasıl toofor Android].</span><span class="sxs-lookup"><span data-stu-id="0b7a6-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Mobile Services'i kullanmaya başlama]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Klasik Azure portalı]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[bildirim hub'ları nasıl toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[Notification Hubs kullanma toopush bildirimleri toousers]: /manage/services/notification-hubs/notify-users-aspnet
[son dakika haberleri Notification Hubs kullanma toosend]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging İstemci Bileşeni]: http://components.xamarin.com/view/GCMClient/
[Azure Mesajlaşma Bileşeni]: http://components.xamarin.com/view/azure-messaging
