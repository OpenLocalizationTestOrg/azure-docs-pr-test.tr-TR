---
title: "Azure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 26ba47b19f3a503693d60d344ad39b9eba74fe99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="93776-103">Android'de Engagement Reach tümleştirme</span><span class="sxs-lookup"><span data-stu-id="93776-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93776-104">Tümleştirme katılım nasıl Android belge üzerinde bu kılavuzu izlemeden önce açıklanan tümleştirme yordamı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="93776-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="93776-105">Standart tümleştirme</span><span class="sxs-lookup"><span data-stu-id="93776-105">Standard integration</span></span>

<span data-ttu-id="93776-106">Projenize SDK ulaşma kaynak dosyalarını kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="93776-106">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="93776-107">Dosyalarından kopyalamak `res/layout` klasörü teslim SDK'sı `res/layout` uygulamanızın klasör.</span><span class="sxs-lookup"><span data-stu-id="93776-107">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="93776-108">Dosyalarından kopyalamak `res/drawable` klasörü teslim SDK'sı `res/drawable` uygulamanızın klasör.</span><span class="sxs-lookup"><span data-stu-id="93776-108">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="93776-109">Düzenleme, `AndroidManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="93776-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="93776-110">Aşağıdaki bölümde ekleyin (arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="93776-110">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* <span data-ttu-id="93776-111">Önyüklemede tıklattınız değil Sistem bildirimleri yeniden yürütme izni gerekir (Aksi halde diskte tutulur ancak artık görüntülenmeyecek, gerçekten bu eklemek zorunda).</span><span class="sxs-lookup"><span data-stu-id="93776-111">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="93776-112">Kopyalama ve aşağıdaki bölümde düzenleme bildirimler (hem de uygulama ve sistem olanlar) için kullanılan bir simge belirtin (arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="93776-112">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="93776-113">Bu bölüm **zorunlu** sistem bildirimleri Reach kampanyaları oluştururken kullanmayı planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="93776-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="93776-114">Android gösterilen gelen sistem bildirimleri simgeler olmadan engeller.</span><span class="sxs-lookup"><span data-stu-id="93776-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="93776-115">Bu nedenle bu bölümde atlarsanız, son kullanıcılarınızın bunları almak mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="93776-115">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="93776-116">Büyük resim kullanarak sistem bildirimleri ile Kampanyalar oluşturursanız, aşağıdaki izinleri ekleyin gerekir (sonra `</application>` etiketi) eksikse:</span><span class="sxs-lookup"><span data-stu-id="93776-116">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="93776-117">Android M ve uygulamanızı Android API düzeyi 23 ya da daha hedefleyip hedeflemediği ``WRITE_EXTERNAL_STORAGE`` izni kullanıcı onayı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="93776-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="93776-118">Lütfen okuyun [Bu bölümde](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="93776-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="93776-119">Sistem bildirimleri için cihazın halka ve/veya Titret Reach kampanya de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93776-119">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="93776-120">Bunun çalışması için aşağıdaki izin bildirildiğinden emin olun zorunda (sonra `</application>` etiketi):</span><span class="sxs-lookup"><span data-stu-id="93776-120">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="93776-121">Bu izin olmadan Android engeller sistem bildirimleri engeller halka veya Reach kampanya Yöneticisi'nde vibrate seçeneğini işaretli gösterilir.</span><span class="sxs-lookup"><span data-stu-id="93776-121">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="93776-122">Yerel gönderim</span><span class="sxs-lookup"><span data-stu-id="93776-122">Native Push</span></span>
<span data-ttu-id="93776-123">Reach modülünün yapılandırılmış, cihazda Kampanyalar şekilde alabilmesi için yerel gönderimi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93776-123">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="93776-124">Android iki hizmet destekliyoruz:</span><span class="sxs-lookup"><span data-stu-id="93776-124">We support two services on Android:</span></span>

* <span data-ttu-id="93776-125">Google Play aygıtları: kullanım [Google Cloud Messaging] izleyerek [tümleştirmek GCM katılım Kılavuzu ile nasıl](mobile-engagement-android-gcm-integrate.md) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="93776-125">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="93776-126">Amazon aygıtları: kullanım [Amazon Device Messaging] izleyerek [tümleştirmek ADM katılım Kılavuzu ile nasıl](mobile-engagement-android-adm-integrate.md) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="93776-126">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="93776-127">Amazon ve Google Play aygıtlar, geliştirme için 1 AndroidManifest.xml/APK içindeki tüm öğeler için olası hedef istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="93776-127">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="93776-128">Ancak GCM kod bulursanız, Amazon gönderirken, bunlar uygulamanızı reddedebilir.</span><span class="sxs-lookup"><span data-stu-id="93776-128">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="93776-129">Bu durumda birden çok APKs kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93776-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="93776-130">**Uygulamanızı şimdi almak ve reach kampanyaları görüntülemek hazır!**</span><span class="sxs-lookup"><span data-stu-id="93776-130">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="93776-131">Veri gönderimi nasıl ele alınacağını</span><span class="sxs-lookup"><span data-stu-id="93776-131">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="93776-132">Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="93776-132">Integration</span></span>
<span data-ttu-id="93776-133">Reach veri gönderimleri almak, uygulamanızın istiyorsanız, bir alt sınıfı oluşturmak zorunda `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` ve içinde referans `AndroidManifest.xml` dosyası (arasında `<application>` ve/veya `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="93776-133">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="93776-134">Geçersiz kılabilirsiniz `onDataPushStringReceived` ve `onDataPushBase64Received` geri aramalar.</span><span class="sxs-lookup"><span data-stu-id="93776-134">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="93776-135">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="93776-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="93776-136">Kategori</span><span class="sxs-lookup"><span data-stu-id="93776-136">Category</span></span>
<span data-ttu-id="93776-137">Kategori parametresi bir veri gönderme kampanya oluşturduğunuzda isteğe bağlıdır ve filtre veri iter sağlar.</span><span class="sxs-lookup"><span data-stu-id="93776-137">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="93776-138">Veri gönderimleri, farklı türlerde işleme birkaç yayın alıcılar varsa kullanışlıdır veya farklı tür itmek istiyorsanız, `Base64` veri ve ayrıştırmadan önce kendi türünü tanımlamak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="93776-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="93776-139">Geri aramalar dönüş parametresi</span><span class="sxs-lookup"><span data-stu-id="93776-139">Callbacks' return parameter</span></span>
<span data-ttu-id="93776-140">Dönüş parametresi düzgün işlenecek yönergelere `onDataPushStringReceived` ve `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="93776-140">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="93776-141">Bir yayın alıcı döndürmelidir `null` içinde veri gönderimi nasıl ele alınacağını bilmiyorsa geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="93776-141">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="93776-142">Kategori veya yayın Alıcınız veri gönderimi işleyip işlemeyeceğini belirlemek için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93776-142">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="93776-143">Yayın alıcı birini döndürmelidir `true` içinde veri gönderimi kabul ederse geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="93776-143">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="93776-144">Yayın alıcı birini döndürmelidir `false` içinde veri gönderimi algılar ancak herhangi bir nedenle atar geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="93776-144">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="93776-145">Örneğin, sonuç `false` zaman alınan veri geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="93776-145">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="93776-146">Bir alıcı döndürür yayın varsa `true` başka döndürür while `false` aynı veri gönderimi için davranış tanımsızdır, hiçbir zaman, yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93776-146">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="93776-147">Dönüş türü yalnızca ulaşma istatistikleri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="93776-147">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="93776-148">`Replied`yayın alıcıları birini ya da döndürülürse artırılır `true` veya `false`.</span><span class="sxs-lookup"><span data-stu-id="93776-148">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="93776-149">`Actioned`yalnızca yayın alıcıları birini döndürülürse artırılır `true`.</span><span class="sxs-lookup"><span data-stu-id="93776-149">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="93776-150">Kampanyalar özelleştirme</span><span class="sxs-lookup"><span data-stu-id="93776-150">How to customize campaigns</span></span>
<span data-ttu-id="93776-151">Kampanyalar özelleştirmek için Reach SDK'ın sağlanan düzenleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93776-151">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="93776-152">Düzenleri kullanılan tüm tanımlayıcıları tutmak ve özellikle metin görünümleri ve görüntü görünümleri için bir tanımlayıcı kullanın görünüm türlerini tutun.</span><span class="sxs-lookup"><span data-stu-id="93776-152">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="93776-153">Bazı görünümler, yalnızca kendi türü değiştirilemez böylece alanları göstermek veya gizlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="93776-153">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="93776-154">Lütfen sağlanan düzenleri görünümünde türünü değiştirmek istiyorsanız, kaynak kodunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="93776-154">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="93776-155">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="93776-155">Notifications</span></span>
<span data-ttu-id="93776-156">Bildirimler iki tür vardır: farklı düzeni dosyaları kullanan sistem ve uygulama içi bildirimler.</span><span class="sxs-lookup"><span data-stu-id="93776-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="93776-157">Sistem bildirimleri</span><span class="sxs-lookup"><span data-stu-id="93776-157">System notifications</span></span>
<span data-ttu-id="93776-158">Sistem bildirimleri kullanmanız gerekir özelleştirmek için **kategorileri**.</span><span class="sxs-lookup"><span data-stu-id="93776-158">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="93776-159">Atlayabilirsiniz [kategorileri](#categories).</span><span class="sxs-lookup"><span data-stu-id="93776-159">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="93776-160">Uygulama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="93776-160">In-app notifications</span></span>
<span data-ttu-id="93776-161">Varsayılan olarak, bir uygulama bildirimi geçerli etkinliği kullanıcı arabirimi sayesinde Android yöntemi dinamik olarak eklenen görünümdür `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="93776-161">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="93776-162">Bu bildirim bir katmana çağrılır.</span><span class="sxs-lookup"><span data-stu-id="93776-162">This is called a notification overlay.</span></span> <span data-ttu-id="93776-163">Uygulamanız herhangi bir düzende değiştirmenizi gerektirmediği için bildirim yer paylaşımları hızlı tümleştirme için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="93776-163">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="93776-164">Bildirim yer paylaşımları görünümünü değiştirmek için yalnızca dosyasını değiştirebilirsiniz `engagement_notification_area.xml` gereksinimlerinize.</span><span class="sxs-lookup"><span data-stu-id="93776-164">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="93776-165">Dosya `engagement_notification_overlay.xml` bir bildirim katmana oluşturmak için kullanılan sunucudur dosyayı içeren `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="93776-165">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="93776-166">(Katmana içinde bildirim alanında konumlandırma ettirilmesi gibi), gereksinimlerinize uyacak şekilde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93776-166">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="93776-167">Bir etkinlik düzeni bir parçası olarak bildirim düzeni içerir</span><span class="sxs-lookup"><span data-stu-id="93776-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="93776-168">Yer paylaşımları hızlı tümleştirme için harika ancak kullanışsız veya özel durumlarda yan etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="93776-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="93776-169">Bir katmana sistem düzeyinde özel etkinlikler için yan etkileri önlemek kolaylaşır bir etkinlik, özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="93776-169">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="93776-170">Varolan düzeninizi Android sayesinde bizim bildirim düzeni dahil karar verebilirler **dahil** deyimi.</span><span class="sxs-lookup"><span data-stu-id="93776-170">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="93776-171">Aşağıdaki değiştirilmiş bir örneğidir `ListActivity` düzenini yalnızca içeren bir `ListView`.</span><span class="sxs-lookup"><span data-stu-id="93776-171">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="93776-172">**Engagement tümleştirmesi önce:**</span><span class="sxs-lookup"><span data-stu-id="93776-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="93776-173">**Engagement tümleştirmesi sonra:**</span><span class="sxs-lookup"><span data-stu-id="93776-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="93776-174">Bu örnekte, özgün düzeni bir liste görünümü en üst düzey öğesi olarak kullanılan bu yana bir üst öğe kapsayıcısı eklediğimiz.</span><span class="sxs-lookup"><span data-stu-id="93776-174">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="93776-175">Ayrıca eklediğimiz `android:layout_weight="1"` ile yapılandırılmış bir liste görünümü aşağıdaki görünüm eklemek için `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="93776-175">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="93776-176">Engagement Reach SDK'sı, bildirim düzeni bu etkinlikte bulunan ve bu etkinlik için bir katmana eklemez otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="93776-176">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="93776-177">Uygulamanızda bir ListActivity kullanırsanız, görünür bir Reach katmana tıkladığınız için liste görünümünde öğeleri artık tepki engeller.</span><span class="sxs-lookup"><span data-stu-id="93776-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="93776-178">Bu bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="93776-178">This is a known issue.</span></span> <span data-ttu-id="93776-179">Bu sorunu çözmek için bildirim düzeni düzeninde kendi listesi etkinliği gibi önceki örnekteki katıştırmak için öneririz.</span><span class="sxs-lookup"><span data-stu-id="93776-179">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="93776-180">Etkinlik başına uygulama bildirimini devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="93776-180">Disabling application notification per activity</span></span>
<span data-ttu-id="93776-181">Etkinliğiniz için eklenecek katmana istemediğiniz ve kendi düzende bildirim düzeni eklemezseniz, bu etkinlik bir katmana devre dışı bırakabilir `AndroidManifest.xml` ekleyerek bir `meta-data` bölümüne aşağıdaki örnekte ister:</span><span class="sxs-lookup"><span data-stu-id="93776-181">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="93776-182"><a name="categories"></a>Kategorileri</span><span class="sxs-lookup"><span data-stu-id="93776-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="93776-183">Sağlanan düzenleri değiştirdiğinizde, tüm bildirimlerinizi görünümünü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="93776-183">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="93776-184">Kategoriler, bildirimler için çeşitli hedeflenen görünüyor (büyük olasılıkla davranışları) tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="93776-184">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="93776-185">Bir kategori Reach kampanya oluşturduğunuzda belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="93776-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="93776-186">Bu belgenin sonraki bölümlerinde açıklanan kategoriler de duyuruları ve yoklamaları, özelleştirmenize olanak tanır olduğunu aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="93776-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="93776-187">Bildirimlerinizi için bir kategori işleyici kaydetmek için uygulama başlatıldığında bir çağrı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="93776-187">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93776-188">Android: işlem özniteliği hakkında uyarı okuyun \<android sdk katılım işlem\> nasıl tümleştirmek engagement Android konuda devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="93776-188">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="93776-189">Aşağıdaki örnek, önceki uyarı onaylanır ve bir alt sınıfı kullanın varsayar `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="93776-189">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="93776-190">`MyNotifier` Nesne, bildirim kategori işleyici uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="93776-190">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="93776-191">Her iki uygulaması olan `EngagementNotifier` arabirimi veya varsayılan uygulaması bir alt sınıfı: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="93776-191">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="93776-192">Aynı bildirim birkaç kategorisi işleyebilir, bunları şöyle kaydedebilirsiniz dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="93776-192">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="93776-193">Varsayılan Kategori uygulaması değiştirmek için aşağıdaki örnekte, uygulamanızı gibi kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="93776-193">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="93776-194">İşleyici kullanılan geçerli kategorisi çoğu yöntemleri içinde geçersiz parametre olarak geçirilen `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="93776-194">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="93776-195">Olarak ya da geçirilir bir `String` parametresi veya dolaylı bir `EngagementReachContent` olan nesne bir `getCategory()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="93776-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="93776-196">Üzerinde yöntemleri tanımlayarak bildirim oluşturma işlemi çoğunu değiştirebilirsiniz `EngagementDefaultNotifier`, daha gelişmiş özelleştirme için teknik belgeler ve kaynak kodu göz çekinmeyin.</span><span class="sxs-lookup"><span data-stu-id="93776-196">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="93776-197">Uygulama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="93776-197">In-app notifications</span></span>
<span data-ttu-id="93776-198">Yalnızca belirli bir kategorideki için alternatif düzenleri kullanmak istiyorsanız, bunu aşağıdaki örnekteki uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="93776-198">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="93776-199">**Örnek `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="93776-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="93776-200">Gördüğünüz gibi katmana görünümü standart olandan farklı tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="93776-200">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="93776-201">Her düzeni yer paylaşımları için benzersiz bir tanımlayıcı kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="93776-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="93776-202">**Örnek `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="93776-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="93776-203">Gördüğünüz gibi bildirim alanında görünümü standart olandan farklı tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="93776-203">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="93776-204">Her düzeni bildirim alanları için benzersiz bir tanımlayıcı kullanır önemlidir.</span><span class="sxs-lookup"><span data-stu-id="93776-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="93776-205">Bu basit örnek kategorisinin ekranın en üstte gösterilen uygulama (veya uygulama) bildirim yapar.</span><span class="sxs-lookup"><span data-stu-id="93776-205">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="93776-206">Bildirim alanında kendisini kullanılan standart tanımlayıcıları değişmemiştir.</span><span class="sxs-lookup"><span data-stu-id="93776-206">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="93776-207">Değiştirmek istediğiniz tanımlanacak varsa `EngagementDefaultNotifier.prepareInAppArea` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="93776-207">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="93776-208">Teknik belgeler ve kaynak kodunu aramak için önerilen `EngagementNotifier` ve `EngagementDefaultNotifier` bu Gelişmiş özelleştirme düzeyi istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="93776-208">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="93776-209">Sistem bildirimleri</span><span class="sxs-lookup"><span data-stu-id="93776-209">System notifications</span></span>
<span data-ttu-id="93776-210">Genişletme tarafından `EngagementDefaultNotifier`, geçersiz kılabilirsiniz `onNotificationPrepared` varsayılan uygulama tarafından hazırlanan bildirim değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="93776-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="93776-211">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="93776-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="93776-212">Bu örnekte "devam eden" kategorisi kullanıldığında, devam eden bir olay görüntülenmesini içerik için bir sistem bildirimi yapar.</span><span class="sxs-lookup"><span data-stu-id="93776-212">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="93776-213">Oluşturmak istiyorsanız `Notification` nesne baştan geri dönebilirsiniz `false` yöntemi ve çağrı `notify` kendiniz `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="93776-213">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="93776-214">Bu durumda, tutmanızı önemli bir `contentIntent`, `deleteIntent` ve tarafından kullanılan bildirim tanımlayıcısı `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="93776-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="93776-215">Bu tür bir uygulama doğru bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="93776-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="93776-216">Yalnızca bildirim duyuruları</span><span class="sxs-lookup"><span data-stu-id="93776-216">Notification only announcements</span></span>
<span data-ttu-id="93776-217">Yalnızca duyuru kılarak özelleştirilebilir bir bildirim tıklayarak Yönetim `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hazırlıklı değiştirmek için `Intent`.</span><span class="sxs-lookup"><span data-stu-id="93776-217">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="93776-218">Bu yöntemi kullanarak bayrakları kolayca ayarlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="93776-218">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="93776-219">Örneğin eklemek `SINGLE_TOP` bayrağı:</span><span class="sxs-lookup"><span data-stu-id="93776-219">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="93776-220">Bu yöntem, eylem URL'si olmadan duyuru kullanılarak çağrılamaz. böylece arka planda ise, sistem bildirimleri eylemi olmadan URL şimdi uygulama başlatma eski katılım kullanıcılar için lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="93776-220">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="93776-221">Bu amaç özelleştirirken düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="93776-221">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="93776-222">Ayrıca uygulayabilirsiniz `EngagementNotifier.executeNotifAnnouncementAction` sıfırdan.</span><span class="sxs-lookup"><span data-stu-id="93776-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="93776-223">Bildirim yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="93776-223">Notification life cycle</span></span>
<span data-ttu-id="93776-224">Varsayılan Kategori kullanırken, bazı yaşam döngüsü yöntemleri üzerinde denir `EngagementReachInteractiveContent` nesne istatistikleri rapor ve kampanya durumunu güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="93776-224">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="93776-225">Bildirim uygulamada görüntülenen ya da durum çubuğunda put `displayNotification` yöntemi (hangi istatistikleri raporları) çağrılır tarafından `EngagementReachAgent` varsa `handleNotification` döndürür `true`.</span><span class="sxs-lookup"><span data-stu-id="93776-225">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="93776-226">Bildirim kapatıldığında, `exitNotification` yöntemi çağrıldığında, istatistik bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="93776-226">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="93776-227">Bildirim tıkladıysanız `actionNotification` olan çağrılır, istatistik bildirilir ve ilişkili amacı başlatılır.</span><span class="sxs-lookup"><span data-stu-id="93776-227">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="93776-228">Uygulamanıza `EngagementNotifier` varsayılan davranışı, atlar başınıza bu yaşam döngüsü yöntemlerini çağırmaya sahip.</span><span class="sxs-lookup"><span data-stu-id="93776-228">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="93776-229">Aşağıdaki örneklerde varsayılan davranış olduğu atlanır bazı durumlarda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="93776-229">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="93776-230">Genişletme yok `EngagementDefaultNotifier`, sıfırdan kategori işleme uygulanan örn.</span><span class="sxs-lookup"><span data-stu-id="93776-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="93776-231">Sistem bildirimleri için geçersiz kılınmış `onNotificationPrepared` ve değiştirdiğiniz `contentIntent` veya `deleteIntent` içinde `Notification` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="93776-231">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="93776-232">Uygulama bildirimleri için geçersiz kılınmış `prepareInAppArea`, en az eşlemek mutlaka `actionNotification` , U.I birine denetler.</span><span class="sxs-lookup"><span data-stu-id="93776-232">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="93776-233">Varsa `handleNotification` bir özel durum, içeriği silinir atar ve `dropContent` olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="93776-233">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="93776-234">Bu durum istatistiklerine bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="93776-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="93776-235">Duyuruları ve yoklamaları</span><span class="sxs-lookup"><span data-stu-id="93776-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="93776-236">Düzenleri</span><span class="sxs-lookup"><span data-stu-id="93776-236">Layouts</span></span>
<span data-ttu-id="93776-237">Değiştirebileceğiniz `engagement_text_announcement.xml`, `engagement_web_announcement.xml` ve `engagement_poll.xml` metin Duyurular, web duyuruları ve yoklamaları özelleştirmek için dosyaları.</span><span class="sxs-lookup"><span data-stu-id="93776-237">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="93776-238">Bu dosyalar başlık alanını ve düğme alanının için iki ortak düzenleri paylaşır.</span><span class="sxs-lookup"><span data-stu-id="93776-238">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="93776-239">Başlığa ilişkin Düzen `engagement_content_title.xml` ve eponymous drawable dosyası için arka plan kullanır.</span><span class="sxs-lookup"><span data-stu-id="93776-239">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="93776-240">Eylem ve çıkış düğmeleri düzeni `engagement_button_bar.xml` ve eponymous drawable dosyası için arka plan kullanır.</span><span class="sxs-lookup"><span data-stu-id="93776-240">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="93776-241">Bir yoklamada soru düzeni ve seçimleri dinamik olarak birkaç kez kullanarak şişirileceğini `engagement_question.xml` sorular için Düzen dosyasını ve `engagement_choice.xml` seçimler dosya.</span><span class="sxs-lookup"><span data-stu-id="93776-241">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="93776-242">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="93776-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="93776-243">Alternatif düzenleri</span><span class="sxs-lookup"><span data-stu-id="93776-243">Alternate layouts</span></span>
<span data-ttu-id="93776-244">Bildirimler gibi kampanya kategori duyuruları ve yoklamaları için alternatif düzenleri sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="93776-244">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="93776-245">Örneğin, bir metin duyuru için bir kategori oluşturmak için genişletebilirsiniz `EngagementTextAnnouncementActivity` ve referans `AndroidManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="93776-245">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="93776-246">Hedefi filtre kategorisinde varsayılan duyuru etkinlik farkı yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="93776-246">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="93776-247">Belirli bir kategorideki sağ etkinliği gidermek için hedefi sistem Reach SDK'sını kullanır ve çözümleme başarısız olursa, geri varsayılan kategorisine göre döner.</span><span class="sxs-lookup"><span data-stu-id="93776-247">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="93776-248">Uygulamak sahip `MyCustomTextAnnouncementActivity`, yalnızca düzenini değiştirme (ancak aynı tanımlayıcılarını görüntüle tutmak) istiyorsanız, yalnızca aşağıdaki örnekte sınıfı gibi tanımlamak gerekir:</span><span class="sxs-lookup"><span data-stu-id="93776-248">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="93776-249">Metin duyuruları varsayılan kategorisini değiştirmek için yalnızca Değiştir `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` , uygulamanız tarafından.</span><span class="sxs-lookup"><span data-stu-id="93776-249">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="93776-250">Web duyuruları ve yoklamaları için benzer bir şekilde özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="93776-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="93776-251">Web duyuruları için genişletebilirsiniz `EngagementWebAnnouncementActivity` ve etkinlik bildirmek `AndroidManifest.xml` aşağıdaki örnekte ister:</span><span class="sxs-lookup"><span data-stu-id="93776-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="93776-252">Anketler için genişletebilirsiniz `EngagementPollActivity` ve declare, içinde `AndroidManifest.xml` aşağıdaki örnekte ister:</span><span class="sxs-lookup"><span data-stu-id="93776-252">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="93776-253">Sıfırdan uygulama</span><span class="sxs-lookup"><span data-stu-id="93776-253">Implementation from scratch</span></span>
<span data-ttu-id="93776-254">Aşağıdakilerden birini genişletmeden duyuru (ve yoklama) etkinliklerinizi için kategoriler uygulayabilirsiniz `Engagement*Activity` Reach SDK tarafından sağlanan sınıfları.</span><span class="sxs-lookup"><span data-stu-id="93776-254">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="93776-255">Örneğin, aynı görünümleri standart düzenleri kullanmayan bir düzen tanımlamak istiyorsanız kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="93776-255">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="93776-256">Gibi gelişmiş bildirim özelleştirme için standart uygulama kaynak koduna bakmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="93776-256">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="93776-257">Göz önünde bulundurmanız gereken bazı şeyler şunlardır: ulaşma içerik tanıtıcısı olan bir ek parametre (hedefi filtre karşılık gelen) belirli bir amaç etkinlikle başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="93776-257">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="93776-258">Kampanya web sitesinde oluşturulurken belirtilen alanları içeren içerik nesnesini almak için bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="93776-258">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="93776-259">STATISTICS için içerik görüntülendiği bildirmelisiniz `onResume` olay:</span><span class="sxs-lookup"><span data-stu-id="93776-259">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="93776-260">Sonra ya da çağırmayı unuttunuz mu `actionContent(this)` veya `exitContent(this)` arka plana etkinlik geçmeden önce içerik nesne üzerinde.</span><span class="sxs-lookup"><span data-stu-id="93776-260">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="93776-261">Ya da yok çağırırsanız `actionContent` veya `exitContent`, istatistikleri (yani bir kampanya hiçbir analytics) gönderilen olmaz ve uygulama işlemini yeniden başlatılana kadar daha da önemlisi, sonraki Kampanyalar bildirilmez.</span><span class="sxs-lookup"><span data-stu-id="93776-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="93776-262">Yönlendirme veya başka yapılandırma değişiklikleri yapabilir kodunu aktivite arka plana veya değil, standart uygulama içeriği kullanıcı etkinliği ayrılsa çıktı olarak bildirilen emin yapar giden olup olmadığını belirlemek hassas ( basarakyada`HOME`veya `BACK`) ancak yönlendirmesini değişirse değil.</span><span class="sxs-lookup"><span data-stu-id="93776-262">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="93776-263">Uygulama ilginç parçası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="93776-263">Here is the interesting part of the implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="93776-264">Aradığınız varsa, gördüğünüz gibi `actionContent(this)` Etkinliğin bitiş sonra `exitContent(this)` herhangi bir etkisi olmadan güvenli bir şekilde çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="93776-264">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
<span data-ttu-id="93776-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span><span class="sxs-lookup"><span data-stu-id="93776-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span></span>
<span data-ttu-id="93776-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span><span class="sxs-lookup"><span data-stu-id="93776-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span></span>
