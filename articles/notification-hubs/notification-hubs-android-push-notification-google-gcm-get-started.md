---
title: "Azure Notification Hubs ile anında iletme bildirimleri tooAndroid aaaSending | Microsoft Docs"
description: "Bu öğreticide, bilgi nasıl toouse Azure Notification Hubs toopush bildirimleri tooAndroid aygıtlar."
services: notification-hubs
documentationcenter: android
keywords: "anında iletme bildirimleri,anında iletme bildirimi,android anında iletme bildirimi"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="5ec8d-104">Azure Notification Hubs ile anında iletme bildirimleri tooAndroid gönderme</span><span class="sxs-lookup"><span data-stu-id="5ec8d-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5ec8d-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5ec8d-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5ec8d-106">Bu konuda Google Cloud Messaging (GCM) ile anında iletme bildirimleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="5ec8d-107">Google Firebase bulut Mesajlaşma (FCM) kullanıyorsanız, bkz: [gönderme anında iletme bildirimleri tooAndroid Azure Notification Hubs ve FCM ile](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="5ec8d-108">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan Android uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-108">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="5ec8d-109">Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan bir Android uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="5ec8d-110">Bu öğreticinin tamamlanan hello kodu Github'dan indirilebilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ec8d-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5ec8d-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5ec8d-112">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="5ec8d-113">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5ec8d-114">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="5ec8d-115">Ayrıca tooan etkin Azure hesabı belirtilen yukarıdaki Bu öğretici yalnızca hello en son sürümünü gerektirir [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-115">In addition tooan active Azure account mentioned above, this tutorial only requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="5ec8d-116">Bu öğreticiyi tamamlamak Android uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="5ec8d-117">Google Cloud Messaging'i destekleyen bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ec8d-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="5ec8d-118">Yeni bir bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5ec8d-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="5ec8d-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="5ec8d-120">Merhaba, **ayarları** dikey penceresinde, select **Bildirim Hizmetleri** ve ardından **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-120">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="5ec8d-121">Merhaba API anahtarını girin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-121">Enter hello API key and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="5ec8d-123">Bildirim hub'ınız şimdi GCM ile yapılandırılmış toowork olduğu ve uygulama tooreceive kaydolun ve anında iletme bildirimleri göndermek hello bağlantı dizeleri tooboth sahip.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-123">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="5ec8d-124"><a id="connecting-app"></a>Uygulama toohello bildirim hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="5ec8d-124"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="5ec8d-125">Yeni bir Android projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ec8d-125">Create a new Android project</span></span>
1. <span data-ttu-id="5ec8d-126">Android Studio'da yeni bir Android Studio projesi başlatın.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - yeni proje][13]
2. <span data-ttu-id="5ec8d-128">Merhaba seçin **telefon ve Tablet** form faktörünü ve hello **Minimum SDK** toosupport istiyor.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-128">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="5ec8d-129">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-129">Then click **Next**.</span></span>
   
   ![Android Studio - proje oluşturma iş akışı][14]
3. <span data-ttu-id="5ec8d-131">Seçin **boş etkinlik** hello ana etkinlik için tıklatın **sonraki**ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-131">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="5ec8d-132">Google Play Hizmetleri toohello proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="5ec8d-132">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="5ec8d-133">Azure Notification Hubs kitaplıkları ekleme</span><span class="sxs-lookup"><span data-stu-id="5ec8d-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="5ec8d-134">Merhaba, `Build.Gradle` hello dosyası **uygulama**, hello satırlarında aşağıdaki hello eklemek **bağımlılıkları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-134">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="5ec8d-135">Depo hello sonra aşağıdaki hello eklemek **bağımlılıkları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-135">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="5ec8d-136">Merhaba AndroidManifest.xml güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-136">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="5ec8d-137">toosupport GCM, biz uygulanmalı bir örnek kimliği dinleme hizmeti çok kullanılan bizim kodda[kayıt belirteçleri elde](https://developers.google.com/cloud-messaging/android/client#sample-register) kullanarak [Google'nın örnek kimliği API'sini](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-137">toosupport GCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="5ec8d-138">Bu öğreticide biz hello sınıfı adlandıracaktır `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-138">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="5ec8d-139">Hizmet tanımı toohello AndroidManifest.xml dosyasına hello aşağıdaki hello eklemek `<application>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-139">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="5ec8d-140">Hello yerine `<your package>` tutucuyla hello hello hello üst kısmında gösterilen asıl Paket adınızla `AndroidManifest.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-140">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="5ec8d-141">Biz örnek kimliği API'sini hello GCM kayıt belirtecimizi aldıktan sonra onu çok kullanacağız[hello Azure bildirim hub'ı ile kayıt](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-141">Once we have received our GCM registration token from hello Instance ID API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="5ec8d-142">Arka plan hello kullanarak Biz bu kayıt destekleyecek bir `IntentService` adlı `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="5ec8d-143">Bu hizmet, [GCM kayıt belirtecimizi yenilemekten](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) de sorumludur.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="5ec8d-144">Hizmet tanımı toohello AndroidManifest.xml dosyasına hello aşağıdaki hello eklemek `<application>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="5ec8d-145">Hello yerine `<your package>` tutucuyla hello hello hello üst kısmında gösterilen asıl Paket adınızla `AndroidManifest.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-145">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="5ec8d-146">Biz de alıcı tooreceive bildirimleri tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-146">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="5ec8d-147">Aşağıdaki alıcı tanımını toohello AndroidManifest.xml dosyasına hello hello eklemek `<application>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-147">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="5ec8d-148">Hello yerine `<your package>` tutucuyla hello hello hello üst kısmında gösterilen asıl Paket adınızla `AndroidManifest.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-148">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="5ec8d-149">Gerekli GCM aşağıdaki hello ilgili hello aşağıdaki izinleri ekleyin `</application>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-149">Add hello following necessary GCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="5ec8d-150">Emin tooreplace olun `<your package>` hello hello üst kısmında gösterilen hello paket adı ile `AndroidManifest.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-150">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="5ec8d-151">Bu izinler hakkında daha fazla bilgi için bkz. [Android için bir GCM İstemcisi uygulaması kurma](https://developers.google.com/cloud-messaging/android/client#manifest).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="5ec8d-152">Kod ekleme</span><span class="sxs-lookup"><span data-stu-id="5ec8d-152">Adding code</span></span>
1. <span data-ttu-id="5ec8d-153">Hello Proje Görünümü'da, genişletin **uygulama** > **src** > **ana** > **java**.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-153">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="5ec8d-154">**Java**'nın altındaki paket klasörünüze sağ tıklayın, **Yeni**'ye tıklayın ve ardından **Java Sınıfı**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="5ec8d-155">`NotificationSettings` adlı yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - yeni Java sınıfı][6]
   
    <span data-ttu-id="5ec8d-157">Tooupdate hello hello kodunu aşağıdaki hello bu üç yer tutucuları emin olun `NotificationSettings` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="5ec8d-157">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="5ec8d-158">**Senderıd**: Merhaba önceki hello elde ettiğiniz proje numarası [Google Cloud Console](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-158">**SenderId**: hello project number you obtained earlier in hello [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="5ec8d-159">**HubListenConnectionString**: Merhaba **DefaultListenAccessSignature** hub'ınız için bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="5ec8d-160">Tıklayarak bağlantı dizesini kopyalayabilirsiniz **erişim ilkeleri** hello üzerinde **ayarları** dikey penceresinde hello üzerinde hub'ınızın [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="5ec8d-160">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="5ec8d-161">**HubName**: hello hub dikey penceresinde hello görünen bildirim hub'ınızın hello adını kullan [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="5ec8d-161">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="5ec8d-162">`NotificationSettings` kodu:</span><span class="sxs-lookup"><span data-stu-id="5ec8d-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="5ec8d-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="5ec8d-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="5ec8d-164">}</span><span class="sxs-lookup"><span data-stu-id="5ec8d-164">}</span></span>
2. <span data-ttu-id="5ec8d-165">Yukarıdaki Hello adımları kullanarak adlı başka bir yeni sınıf ekleyin `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-165">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="5ec8d-166">Bu bizim Örnek Kimliği dinleme hizmeti uygulamamız olacak.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="5ec8d-167">Bu sınıfın Hello kodu çağıracaktır bizim `IntentService` çok[yenileme hello GCM belirtecini](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) hello arka planda.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-167">hello code for this class will call our `IntentService` too[refresh hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="5ec8d-168">Adlı başka bir yeni sınıf tooyour projesi eklemek `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-168">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="5ec8d-169">Bu hello uygulaması olacak bizim `IntentService` işleyecek [yenileme hello GCM belirtecini](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) ve [hello bildirim hub'kaydetme](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-169">This will be hello implementation for our `IntentService` that will handle [refreshing hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="5ec8d-170">Bu sınıfın kodu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-170">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="5ec8d-171">İçinde `MainActivity` sınıfı, hello aşağıdakileri ekleyin `import` deyimleri hello yukarıda sınıf bildiriminin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-171">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="5ec8d-172">Özel üyelerin hello sınıfı hello üstündeki aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-172">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="5ec8d-173">Bunları kullanırız [hello Google Play Hizmetleri'nin kullanılabilirliğini Google tarafından önerildiği şekilde denetlemek](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-173">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="5ec8d-174">İçinde `MainActivity` sınıfı, yöntemi toohello Google Play Hizmetleri'nin kullanılabilirliğini izleyen hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-174">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="5ec8d-175">İçinde `MainActivity` sınıfı, çağırmadan önce Google Play Hizmetleri'ni denetleyecek koddan hello eklemek, `IntentService` tooget GCM kayıt belirtecinizi ve bildirim hub'ınızı ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-175">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="5ec8d-176">Merhaba, `OnCreate` hello yöntemi `MainActivity` sınıfı, etkinlik oluşturulduğunda kod toostart hello kayıt işlemi aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-176">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="5ec8d-177">Bu ek yöntemleri toohello ekleme `MainActivity` uygulamanızda tooverify uygulama durumu ve rapor durumu.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-177">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="5ec8d-178">Merhaba `ToastNotify` yöntemi kullanan hello *"Hello World"* `TextView` kontrol tooreport durumunu ve bildirimleri hello uygulamasında kalıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-178">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="5ec8d-179">Activity_main.xml düzeninizde, bu denetim için kimliği hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-179">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="5ec8d-180">Merhaba AndroidManifest.xml tanımladığımız bizim alıcısı için bir alt sınıfı sonraki ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-180">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="5ec8d-181">Adlı başka bir yeni sınıf tooyour projesi eklemek `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-181">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="5ec8d-182">İçeri aktarma deyimlerini hello üst kısmındaki aşağıdaki hello eklemek `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="5ec8d-182">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="5ec8d-183">Merhaba kodunu aşağıdaki hello eklemek `MyHandler` öğesinin bir alt kolaylaştırarak sınıfı `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-183">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="5ec8d-184">Bu kod hello geçersiz kılmaları `OnReceive` hello işleyici alınan bildirimleri bildirmesi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-184">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="5ec8d-185">Merhaba işleyici ayrıca hello kullanarak hello anında iletme bildirimi toohello Android bildirim Yöneticisi gönderir `sendNotification()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-185">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="5ec8d-186">Merhaba `sendNotification()` yöntemi hello uygulama çalışmıyorken ve bir bildirim alındığında yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-186">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="5ec8d-187">Merhaba menü çubuğunda Android Studio'da sırasıyla **yapı** > **projeyi** toomake kodunuzda hiçbir hata bulunmadığından emin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-187">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="5ec8d-188">Anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="5ec8d-188">Sending push notifications</span></span>
<span data-ttu-id="5ec8d-189">Merhaba göndererek uygulamanızda anında iletme bildirimleri almayı test edebilirsiniz [Azure Portal] -Merhaba Ara **sorun giderme** bölümünde hello hub dikey penceresinde, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-189">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Azure Notification Hubs - Test Gönderimi](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="5ec8d-191">(İsteğe bağlı) Doğrudan hello uygulamadan anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="5ec8d-191">(Optional) Send push notifications directly from hello app</span></span>
<span data-ttu-id="5ec8d-192">Normalde bildirimleri bir arka uç sunucusu kullanarak gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="5ec8d-193">Bazı durumlarda, toobe mümkün toosend anında iletme bildirimleri hello istemci uygulamasından doğrudan isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-193">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="5ec8d-194">Bu bölümde, nasıl toosend bildirimleri kullanan hello istemciden hello açıklanmaktadır [Azure bildirim hub'ı REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ec8d-194">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="5ec8d-195">Android Studio Proje Görünümü'nde, **App** > **src** > **main** > **res** > **layout**'u genişletin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="5ec8d-196">Açık hello `activity_main.xml` düzeni dosya ve hello tıklatın **metin** sekmesinde hello dosyasının tooupdate hello metin içeriği.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-196">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="5ec8d-197">Aşağıdaki hello kodu ile yeni ekleyen güncelleştirmek `Button` ve `EditText` göndermek için denetimleri anında bildirim iletileri toohello bildirim hub'ı.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-197">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="5ec8d-198">Bu kod hello altındaki hemen önüne ekleyin `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-198">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="5ec8d-199">Android Studio Proje Görünümü'nde **App** > **src** > **main** > **res** > **values**'u genişletin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="5ec8d-200">Açık hello `strings.xml` dosya ve hello yeni tarafından başvurulan hello dize değerlerini ekleyin `Button` ve `EditText` kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-200">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="5ec8d-201">Bunlar hello dosyasının hello altındaki hemen önüne ekleyin `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-201">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="5ec8d-202">İçinde `NotificationSetting.java` dosya, ayar toohello aşağıdaki hello eklemek `NotificationSettings` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-202">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="5ec8d-203">Güncelleştirme `HubFullAccess` hello ile **DefaultFullSharedAccessSignature** hub'ınız için bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-203">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="5ec8d-204">Bu bağlantı dizesi hello kopyalanabilir [Azure Portal] tıklayarak **erişim ilkeleri** hello üzerinde **ayarları** dikey bildirim hub'ınız için.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-204">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="5ec8d-205">İçinde `MainActivity.java` dosya, hello aşağıdakileri ekleyin `import` deyimleri hello yukarıda `MainActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-205">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="5ec8d-206">İçinde `MainActivity.java` dosya, üyeleri hello hello üstündeki aşağıdaki hello eklemek `MainActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-206">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="5ec8d-207">Bir POST isteği toosend iletileri tooyour bildirim hub'ı bir yazılım erişim imzası (SaS) belirteci tooauthenticate oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-207">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="5ec8d-208">Bu hello anahtar veri hello bağlantı dizesinden ayrıştırarak yapılır ve ardından oluşturarak hello SaS belirteci hello belirtildiği gibi [ortak kavramlar](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API Başvurusu.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-208">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="5ec8d-209">koddan hello örnek bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-209">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="5ec8d-210">İçinde `MainActivity.java`, yöntem toohello aşağıdaki hello eklemek `MainActivity` tooparse bağlantı dizenizi sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-210">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="5ec8d-211">İçinde `MainActivity.java`, yöntem toohello aşağıdaki hello eklemek `MainActivity` sınıfı toocreate bir SaS kimlik doğrulama belirteci.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-211">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="5ec8d-212">İçinde `MainActivity.java`, yöntemi toohello aşağıdaki hello eklemek `MainActivity` sınıfı toohandle hello **bildirim gönder** düğmesini tıklatın ve yerleşik REST API'sini kullanarak ileti toohello hub hello hello anında iletme bildirimi gönderin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-212">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="5ec8d-213">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="5ec8d-213">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="5ec8d-214">Merhaba öykünücüde anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="5ec8d-214">Push notifications in hello emulator</span></span>
<span data-ttu-id="5ec8d-215">Tootest anında iletme bildirimlerini bir öykünücüde isterseniz öykünücü görüntünüzün, uygulamanız için seçtiğiniz hello Google API düzeyini desteklediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-215">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="5ec8d-216">Görüntünüzü yerel Google API'lerini desteklemiyorsa, hello ile karşılaşırsınız **hizmet\_değil\_kullanılabilir** özel durum.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-216">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="5ec8d-217">Buna ek olarak toohello yukarıdaki emin öykünücüsü altında çalışan, Google hesabı tooyour eklediğiniz **ayarları** > **hesapları**.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-217">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="5ec8d-218">Aksi takdirde, deneme tooregister GCM ile hello sonuçlanabilir **kimlik doğrulaması\_başarısız** özel durum.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-218">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="5ec8d-219">Çalışan hello uygulama</span><span class="sxs-lookup"><span data-stu-id="5ec8d-219">Running hello application</span></span>
1. <span data-ttu-id="5ec8d-220">Merhaba uygulamayı çalıştırın ve hello kayıt kimliği başarılı bir kaydı bildirdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-220">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
      ![Android'de test etme - Kanal kaydı][18]
2. <span data-ttu-id="5ec8d-222">Merhaba hub'da kayıtlı Android cihazlar tooall gönderilen bir bildirim iletisi toobe girin.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-222">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
      ![Andorid'de test etme - bir ileti gönderme][19]

3. <span data-ttu-id="5ec8d-224">**Bildirim Gönder**'e basın.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-224">Press **Send Notification**.</span></span> <span data-ttu-id="5ec8d-225">Merhaba uygulamasının çalışıyor cihazlarını göstermeyecektir bir `AlertDialog` hello anında iletme bildirimi iletisi örneğiyle.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-225">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="5ec8d-226">Merhaba uygulamasının çalışıyor yoksa, ancak daha önce kaydolan cihazlar anında iletme bildirimleri için hello Android bildirim Yöneticisi bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-226">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="5ec8d-227">Bu, hello sol üst köşeden aşağı çekilerek görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-227">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
      ![Android'de test etme - bildirimler][21]

## <a name="next-steps"></a><span data-ttu-id="5ec8d-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ec8d-229">Next steps</span></span>
<span data-ttu-id="5ec8d-230">Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers] hello sonraki adım olarak Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-230">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="5ec8d-231">Bunu nasıl kullanarak bir ASP.NET arka uç toosend bildirimleri etiketler tootarget belirli kullanıcılara gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-231">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="5ec8d-232">Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız, hello denetleyin [son dakika haberleri Notification Hubs kullanma toosend] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="5ec8d-232">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="5ec8d-233">toolearn Notification Hubs hakkında daha fazla genel bilgi bizim [Notification Hubs Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="5ec8d-233">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs kullanma toopush bildirimleri toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com
