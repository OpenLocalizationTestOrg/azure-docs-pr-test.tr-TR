---
title: "Azure Notification Hubs ve Firebase Cloud Messaging ile Android'e anında iletme bildirimleri gönderme | Microsoft Belgeleri"
description: "Bu öğreticide, Android cihazlarına anında iletme bildirimleri göndermek için Azure Notification Hubs ve Firebase Cloud Messaging’in nasıl kullanılacağını öğrenirsiniz."
services: notification-hubs
documentationcenter: android
keywords: "anında iletme bildirimleri,anında iletme bildirimi,android anında iletme bildirimi,fcm,firebase cloud messaging"
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: 45a3fa5c7190e039fd637c78a41eeb3f6ede9bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="52673-104">Azure Notification Hubs ile Android'e anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="52673-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="52673-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="52673-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="52673-106">Bu konuda Google Firebase Cloud Messaging (FCM) ile anında iletme bildirimleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="52673-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="52673-107">Hala Google Cloud Messaging (GCM) kullanıyorsanız bkz. [Azure Notification Hubs ve GCM ile Android’e anında iletme bildirimleri gönderme](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="52673-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="52673-108">Bu öğreticide, bir Android uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs ve Firebase Cloud Messaging'in nasıl kullanılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="52673-108">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to send push notifications to an Android application.</span></span>
<span data-ttu-id="52673-109">Firebase Cloud Messaging (FCM) kullanarak anında iletme bildirimleri alan bir Android uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="52673-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="52673-110">Bu öğreticinin tamamlanan kodu GitHub'da [buradan](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase) indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="52673-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52673-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="52673-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="52673-112">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="52673-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="52673-113">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52673-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="52673-114">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="52673-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="52673-115">Yukarıda belirtilen etkin bir Azure hesabının yanı sıra, bu öğretici [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)'nun en son sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="52673-115">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="52673-116">Firebase Cloud Messaging için Android 2.3 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="52673-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="52673-117">Firebase Cloud Messaging için Google Deposu düzeltme 27 gereklidir.</span><span class="sxs-lookup"><span data-stu-id="52673-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="52673-118">Firebase Cloud Messaging için Google Play Services 9.0.2 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="52673-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="52673-119">Bu öğreticiyi tamamlamak Android uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="52673-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="52673-120">Yeni bir Android Studio Projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="52673-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="52673-121">Android Studio'da yeni bir Android Studio projesi başlatın.</span><span class="sxs-lookup"><span data-stu-id="52673-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="52673-122">**Telefon ve Tablet** form faktörünü ve desteklemek istediğiniz **Minimum SDK**'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="52673-122">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="52673-123">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52673-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="52673-124">Ana etkinlik için **Boş Etkinlik**'i seçin, **İleri**'ye tıklayın ve ardından **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52673-124">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="52673-125">Firebase Cloud Messaging'i destekleyen bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="52673-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="52673-126">Yeni bir bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52673-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="52673-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="52673-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="52673-128">Bildirim hub’ınızın **Ayarlar** dikey penceresinde **Bildirim Hizmetleri**'ni ve ardından **Google (GCM)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-128">In the **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="52673-129">Daha önce [Firebase konsolundan](https://firebase.google.com/console/) kopyaladığınız FCM sunucu anahtarını girin ve **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52673-129">Enter the FCM server key you copied earlier from the [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="52673-131">Bildirim hub'ınız şimdi Firebase Cloud Messaging ile birlikte çalışmak üzere yapılandırıldı. Uygulamanızı anında iletme bildirimleri alması ve göndermesi amacıyla kaydetmek için bağlantı dizelerine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="52673-131">Your notification hub is now configured to work with Firebase Cloud Messagin, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="52673-132"><a id="connecting-app"></a>Uygulamanızı bildirim hub'ına bağlama</span><span class="sxs-lookup"><span data-stu-id="52673-132"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="52673-133">Projeye Google Play hizmetlerini ekleme</span><span class="sxs-lookup"><span data-stu-id="52673-133">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="52673-134">Azure Notification Hubs kitaplıkları ekleme</span><span class="sxs-lookup"><span data-stu-id="52673-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="52673-135">**Uygulamanın** `Build.Gradle` dosyasında **bağımlılıklar** bölümüne aşağıdaki satırları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-135">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="52673-136">**Bağımlılıklar** bölümünden sonra aşağıdaki depoyu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-136">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="52673-137">AndroidManifest.xml'i güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="52673-137">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="52673-138">FCM'yi desteklemek için kodumuza, [Google'ın FirebaseInstanceId API'sini](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId) kullanarak [kayıt belirteçleri elde etmek](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) için kullanılan bir Örnek Kimliği dinleme hizmeti eklememiz gereklidir.</span><span class="sxs-lookup"><span data-stu-id="52673-138">To support FCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="52673-139">Bu öğreticide sınıfa `MyInstanceIDService` adını vereceğiz.</span><span class="sxs-lookup"><span data-stu-id="52673-139">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="52673-140">Aşağıdaki hizmet tanımını AndroidManifest.xml dosyasında `<application>` etiketinin içine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-140">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="52673-141">FirebaseInstanceId API'sinden FCM kayıt belirtecimizi aldıktan sonra, [Azure Notification Hub'a kaydolmak](notification-hubs-push-notification-registration-management.md) için bu belirteci kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="52673-141">Once we have received our FCM registration token from the FirebaseInstanceId API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="52673-142">`RegistrationIntentService` adlı bir `IntentService` kullanarak bu kaydı arka planda destekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="52673-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="52673-143">Bu hizmet, FCM kayıt belirtecimizi yenilemekten de sorumludur.</span><span class="sxs-lookup"><span data-stu-id="52673-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="52673-144">Aşağıdaki hizmet tanımını AndroidManifest.xml dosyasında `<application>` etiketinin içine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="52673-145">Bildirimleri almak için bir alıcı da tanımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="52673-145">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="52673-146">Aşağıdaki alıcı tanımını AndroidManifest.xml dosyasına `<application>` etiketinin içine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-146">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="52673-147">`<your package>` yer tutucusunu, `AndroidManifest.xml` dosyasının üst kısmında gösterilen asıl paket adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="52673-147">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="52673-148">Aşağıdaki FCM ile ilgili gerekli izinleri `</application>` etiketinin altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-148">Add the following necessary FCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="52673-149">`<your package>` öğesini, `AndroidManifest.xml` dosyasının üst kısmında gösterilen paket adıyla değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="52673-149">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="52673-150">Bu izinler hakkında daha fazla bilgi için bkz. [Android için GCM İstemci uygulaması ayarlama](https://developers.google.com/cloud-messaging/android/client#manifest) ve [Android için GCM İstemci Uygulamasını Firebase Cloud Messaging’e geçirme](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="52673-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="52673-151">Kod ekleme</span><span class="sxs-lookup"><span data-stu-id="52673-151">Adding code</span></span>
1. <span data-ttu-id="52673-152">Proje Görünümü'nde **app** > **src** > **main** > **java**'yı genişletin.</span><span class="sxs-lookup"><span data-stu-id="52673-152">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="52673-153">**Java**'nın altındaki paket klasörünüze sağ tıklayın, **Yeni**'ye tıklayın ve ardından **Java Sınıfı**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52673-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="52673-154">`NotificationSettings` adlı yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - yeni Java sınıfı](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="52673-156">Aşağıdaki kodda `NotificationSettings` sınıfı için bu üç yer tutucuyu güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="52673-156">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="52673-157">**SenderId**: [Firebase konsolundaki](https://firebase.google.com/console/) proje ayarlarınızın **Cloud Messaging** sekmesinde daha önce edindiğiniz Gönderen Kimliği.</span><span class="sxs-lookup"><span data-stu-id="52673-157">**SenderId**: The Sender Id you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="52673-158">**HubListenConnectionString**: Hub'ınız için **DefaultListenAccessSignature** bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="52673-158">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="52673-159">[Azure Portal]'da hub'ınızın **Ayarlar** dikey penceresinde bulunan **Erişim İlkeleri**'ne tıklayarak bağlantı dizesini kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52673-159">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="52673-160">**HubName**: [Azure Portal]'daki hub dikey penceresinde görünen bildirim hub'ınızın adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="52673-160">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="52673-161">`NotificationSettings` kodu:</span><span class="sxs-lookup"><span data-stu-id="52673-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="52673-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="52673-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="52673-163">}</span><span class="sxs-lookup"><span data-stu-id="52673-163">}</span></span>
2. <span data-ttu-id="52673-164">Yukarıdaki adımları kullanarak `MyInstanceIDService` adlı yeni bir sınıf daha ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-164">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="52673-165">Bu bizim Örnek Kimliği dinleme hizmeti uygulamamız olacak.</span><span class="sxs-lookup"><span data-stu-id="52673-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="52673-166">Bu sınıfın kodu, arka planda `IntentService`FCM belirtecini yenileme[ amacıyla ](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) hizmetimizi çağırır.</span><span class="sxs-lookup"><span data-stu-id="52673-166">The code for this class will call our `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="52673-167">`RegistrationIntentService` adlı projenize, başka bir yeni sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-167">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="52673-168">Bu, [FCM belirtecini yenileme](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) ve [bildirim hub'ıyla kayıt yapma](notification-hubs-push-notification-registration-management.md) işlemlerini ele alacak `IntentService` hizmetimizin uygulanması olacak.</span><span class="sxs-lookup"><span data-stu-id="52673-168">This will be the implementation for our `IntentService` that will handle [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="52673-169">Bu sınıf için aşağıdaki kod kullanın.</span><span class="sxs-lookup"><span data-stu-id="52673-169">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
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
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if the token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete registration", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="52673-170">`MainActivity` sınıfınızda aşağıdaki `import` deyimlerini sınıf bildiriminin üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-170">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="52673-171">Aşağıdaki özel üyeleri sınıfın en üst kısmına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-171">Add the following private members at the top of the class.</span></span> <span data-ttu-id="52673-172">[Google Play Hizmetleri'nin kullanılabilirliğini Google tarafından önerildiği şekilde denetlemek](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk) için bunları kullanırız.</span><span class="sxs-lookup"><span data-stu-id="52673-172">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="52673-173">`MainActivity` sınıfınızda Google Play Hizmetleri'nin kullanılabilirliğine aşağıdaki yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-173">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
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
5. <span data-ttu-id="52673-174">`MainActivity` sınıfınızda, FCM kayıt belirtecinizi almak ve bildirim hub'ınızla kaydolmak için `IntentService` hizmetinizi çağırmadan önce Google Play Hizmetleri'ni denetleyecek aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-174">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="52673-175">`MainActivity` sınıfının `OnCreate` yönteminde, etkinlik oluşturulduğunda kayıt işlemini başlatmak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-175">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="52673-176">Uygulama durumunu doğrulamak ve uygulamanızda durumu raporlamak için bu ek yöntemleri `MainActivity` öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-176">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="52673-177">`ToastNotify` yöntemi, uygulamada kalıcı olarak durumu ve bildirimleri raporlamak için *"Hello World"* `TextView` denetimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="52673-177">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="52673-178">activity_main.xml düzeninizde bu denetim için aşağıdaki kimliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-178">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="52673-179">Ardından, AndroidManifest.xml'de tanımladığımız alıcımız için bir alt sınıf ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="52673-179">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="52673-180">`MyHandler` adlı projenize başka bir yeni sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-180">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="52673-181">`MyHandler.java`'in üst kısmına şu içeri aktarma deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="52673-181">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="52673-182">`MyHandler` sınıfı için aşağıdaki kodu ekleyip bunu `com.microsoft.windowsazure.notifications.NotificationsHandler` öğesinin bir alt sınıfı haline getirin.</span><span class="sxs-lookup"><span data-stu-id="52673-182">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="52673-183">Bu kod, `OnReceive` yöntemini geçersiz kılar; böylece işleyici alınan bildirimleri raporlar.</span><span class="sxs-lookup"><span data-stu-id="52673-183">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="52673-184">İşleyici, `sendNotification()` yöntemini kullanarak Android bildirim yöneticisine anında iletme bildirimi gönderir.</span><span class="sxs-lookup"><span data-stu-id="52673-184">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="52673-185">`sendNotification()` yöntemi, uygulama çalışmıyorken ve bir bildirim alındığında yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="52673-185">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="52673-186">Android Studio'nun menü çubuğunda, kodunuzda hiçbir hata bulunmadığından emin olmak için **Oluştur** > **Projeyi Yeniden Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52673-186">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="52673-187">Cihazınızda uygulamayı çalıştırın ve uygulamanın bildirim hub'ına başarıyla kaydolduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="52673-187">Run the app on your device and verify it registers successfully with the notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="52673-188">Kayıt, örnek kimlik hizmetinin `onTokenRefresh()` yöntemi çağrılana kadar ilk başlatmada başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="52673-188">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="52673-189">Yenileme işlemi bildirim hub’ına başarılı bir kayıt başlatmalıdır.</span><span class="sxs-lookup"><span data-stu-id="52673-189">The refresh should intiate a successful registration with the notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="52673-190">Anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="52673-190">Sending push notifications</span></span>
<span data-ttu-id="52673-191">Uygulamanızda anında iletme bildirimlerini aldığınızı, bunları [Azure Portal] aracılığıyla göndererek test edebilirsiniz; aşağıda gösterildiği gibi hub dikey penceresinin **Sorun Giderme** Bölümü'nü bulun.</span><span class="sxs-lookup"><span data-stu-id="52673-191">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure Notification Hubs - Test Gönderimi](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="52673-193">(İsteğe bağlı) Doğrudan uygulamadan anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="52673-193">(Optional) Send push notifications directly from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="52673-194">İstemci uygulamasından bildirim göndermeye yönelik bu örnek yalnızca öğrenme amacıyla verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="52673-194">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="52673-195">Bu işlem istemci uygulamada `DefaultFullSharedAccessSignature` gerektireceğinden, bildirim hub’ınızı bir kullanıcının istemcilerinize yetkisiz bildirimler göndermek üzere erişim kazanabilmesi riskine maruz bırakır.</span><span class="sxs-lookup"><span data-stu-id="52673-195">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="52673-196">Normalde bildirimleri bir arka uç sunucusu kullanarak gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52673-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="52673-197">Bazı durumlarda, anında iletme bildirimlerini doğrudan istemci uygulamasından gönderebilmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52673-197">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="52673-198">Bu bölüm, [Azure Notification Hubs REST API'si](https://msdn.microsoft.com/library/azure/dn223264.aspx) kullanarak istemciden nasıl bildirim gönderildiğini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="52673-198">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="52673-199">Android Studio Proje Görünümü'nde, **App** > **src** > **main** > **res** > **layout**'u genişletin.</span><span class="sxs-lookup"><span data-stu-id="52673-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="52673-200">`activity_main.xml` düzen dosyasını açın ve dosyanın metin içeriğini güncelleştirmek için **Metin** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52673-200">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="52673-201">Bildirim hub'ına anında iletme bildirimi iletileri göndermek için yeni `Button` ve `EditText` denetimlerini ekleyen aşağıdaki kod ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="52673-201">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="52673-202">Bu kodu en alta, `</RelativeLayout>` öğesinin hemen önüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-202">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="52673-203">Android Studio Proje Görünümü'nde **App** > **src** > **main** > **res** > **values**'u genişletin.</span><span class="sxs-lookup"><span data-stu-id="52673-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="52673-204">`strings.xml` dosyasını açın ve yeni `Button` ve `EditText` denetimleri tarafından başvurulan dize değerlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-204">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="52673-205">Bunları dosyanın en altına, `</resources>` öğesinin hemen önüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-205">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="52673-206">`NotificationSetting.java` dosyanızda `NotificationSettings` sınıfına aşağıdaki ayarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-206">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="52673-207">`HubFullAccess` öğesini, **DefaultFullSharedAccessSignature** bağlantı dizesiyle hub'ınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="52673-207">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="52673-208">Bu bağlantı dizesi, bildirim hub'ınızın **Ayarlar** dikey penceresinde **Erişim İlkeleri**'ne tıklanarak [Azure Portal]'dan kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="52673-208">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="52673-209">`MainActivity.java` dosyanızda aşağıdaki `import` deyimlerini `MainActivity` sınıfının üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-209">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="52673-210">`MainActivity.java` dosyanızda aşağıdaki üyeleri `MainActivity` sınıfının üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-210">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="52673-211">Bildirim hub'ınıza ileti göndermek amacıyla bir POST isteğinin kimlik doğrulamasını yapmak için bir Yazılım Erişim İmzası (SaS) belirteci oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="52673-211">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="52673-212">Bu, anahtar verilerini bağlantı dizesinden ayrıştırarak ve ardından [Ortak Kavramlar](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API'si başvurusunda belirtildiği gibi SaS belirtecini oluşturarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="52673-212">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="52673-213">Aşağıdaki kod örnek bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="52673-213">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="52673-214">Bağlantı dizenizi ayrıştırmak için `MainActivity.java` öğesinde aşağıdaki yöntemi `MainActivity` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-214">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
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
7. <span data-ttu-id="52673-215">Bir SaS kimlik doğrulaması belirteci oluşturmak için `MainActivity.java` öğesinde aşağıdaki yöntemi `MainActivity` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-215">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
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
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
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
8. <span data-ttu-id="52673-216">**Bildirim Gönder** düğmesine tıklanmasını ele almak ve yerleşik REST API'sini kullanarak hub'a anında iletme bildirimi iletisi göndermek için `MainActivity.java` öğesinde `MainActivity` sınıfına aşağıdaki yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="52673-216">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
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
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="52673-217">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="52673-217">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="52673-218">Öykünücüde anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="52673-218">Push notifications in the emulator</span></span>
<span data-ttu-id="52673-219">Anında iletme bildirimlerini bir öykünücüde test etmek isterseniz öykünücü görüntünüzün, uygulamanız için seçtiğiniz Google API düzeyini desteklediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="52673-219">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="52673-220">Görüntünüz yerel Google API'lerini desteklemiyorsa **HİZMET\_\_KULLANILAMIYOR** özel durumuyla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="52673-220">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="52673-221">Yukarıdakine ek olarak, **Ayarlar** > **Hesaplar**'ın altında çalışan öykünücünüze Google hesabınızı eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="52673-221">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="52673-222">Aksi halde, GCM ile kayıt girişimleriniz **KİMLİK DOĞRULAMASI\_BAŞARISIZ** özel durumuyla sonuçlanabilir.</span><span class="sxs-lookup"><span data-stu-id="52673-222">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="52673-223">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="52673-223">Running the application</span></span>
1. <span data-ttu-id="52673-224">Uygulamayı çalıştırın ve kayıt kimliğinin başarılı bir kaydı bildirdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="52673-224">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="52673-225">Hub'da kayıtlı tüm Android cihazlara gönderilecek bir bildirim iletisi girin.</span><span class="sxs-lookup"><span data-stu-id="52673-225">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="52673-226">**Bildirim Gönder**'e basın.</span><span class="sxs-lookup"><span data-stu-id="52673-226">Press **Send Notification**.</span></span> <span data-ttu-id="52673-227">Uygulamayı çalıştıran tüm cihazlarda, anında iletme bildirimi iletisiyle birlikte bir `AlertDialog` örneği görünür.</span><span class="sxs-lookup"><span data-stu-id="52673-227">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="52673-228">Uygulamayı çalıştırmayan ancak anında iletme bildirimleri için daha önce kaydolan cihazlar, Android Bildirim Yöneticisi'nde bir bildirim alır.</span><span class="sxs-lookup"><span data-stu-id="52673-228">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="52673-229">Bunlar, sol üst köşeden aşağı çekilerek görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="52673-229">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="52673-230">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52673-230">Next steps</span></span>
<span data-ttu-id="52673-231">Sonraki adım olarak [Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma] öğreticisini öneririz.</span><span class="sxs-lookup"><span data-stu-id="52673-231">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="52673-232">Bu, belirli kullanıcıları hedeflemek için etiketler kullanarak ASP.NET arka ucundan nasıl bildirim göndereceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="52673-232">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="52673-233">Kullanıcılarınızı ilgi alanı gruplarına göre segmentlere ayırmak istiyorsanız [Son dakika haberleri göndermek için Notification Hubs kullanma] öğreticisine göz atın.</span><span class="sxs-lookup"><span data-stu-id="52673-233">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="52673-234">Notification Hubs hakkında daha fazla genel bilgi edinmek için bkz. [Notification Hubs Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="52673-234">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="52673-235">[Notification Hubs Kılavuzu]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="52673-235">[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="52673-236">[Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="52673-236">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="52673-237">[Son dakika haberleri göndermek için Notification Hubs kullanma]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="52673-237">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="52673-238">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="52673-238">[Azure Portal]: https://portal.azure.com</span></span>
