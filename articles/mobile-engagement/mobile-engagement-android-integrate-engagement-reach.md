---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
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
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="be148-103">TooIntegrate Engagement Reach nasıl Android</span><span class="sxs-lookup"><span data-stu-id="be148-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="be148-104">TooIntegrate android'de katılım nasıl belge bu kılavuzu izlemeden önce hello açıklanan hello tümleştirme yordamı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="be148-105">Standart tümleştirme</span><span class="sxs-lookup"><span data-stu-id="be148-105">Standard integration</span></span>

<span data-ttu-id="be148-106">Projenizdeki hello SDK ulaşma kaynak dosyalarını kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="be148-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="be148-107">Hello Hello dosyaları kopyalamak `res/layout` klasörü teslim hello içine hello SDK ile `res/layout` uygulamanızın klasör.</span><span class="sxs-lookup"><span data-stu-id="be148-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="be148-108">Hello Hello dosyaları kopyalamak `res/drawable` klasörü teslim hello içine hello SDK ile `res/drawable` uygulamanızın klasör.</span><span class="sxs-lookup"><span data-stu-id="be148-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="be148-109">Düzenleme, `AndroidManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="be148-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="be148-110">Ekle bölümden hello (Merhaba arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="be148-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="be148-111">Önyüklemede tıklattınız değil bu izni tooreplay sistem bildirimleri gerekir (Aksi halde diskte tutulur ancak artık görüntülenmeyecek, gerçekten tooinclude bu gerekir).</span><span class="sxs-lookup"><span data-stu-id="be148-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="be148-112">Kopyalama ve bölümden hello düzenleme bildirimler (hem de uygulama ve sistem olanlar) için kullanılan bir simge belirtin (Merhaba arasında `<application>` ve `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="be148-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="be148-113">Bu bölüm **zorunlu** sistem bildirimleri Reach kampanyaları oluştururken kullanmayı planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="be148-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="be148-114">Android gösterilen gelen sistem bildirimleri simgeler olmadan engeller.</span><span class="sxs-lookup"><span data-stu-id="be148-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="be148-115">Bu bölümde atlarsanız, son kullanıcılarınıza mümkün tooreceive olmayacak şekilde bunları.</span><span class="sxs-lookup"><span data-stu-id="be148-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="be148-116">Büyük resim kullanarak sistem bildirimleri ile Kampanyalar oluşturursanız, aşağıdaki izinleri tooadd hello gerekir (Merhaba sonra `</application>` etiketi) eksikse:</span><span class="sxs-lookup"><span data-stu-id="be148-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="be148-117">Android M ve uygulamanızı Android API düzeyi 23 ya da daha hedefleyip hedeflemediği ``WRITE_EXTERNAL_STORAGE`` izni kullanıcı onayı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be148-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="be148-118">Lütfen okuyun [Bu bölümde](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="be148-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="be148-119">Ayrıca hello belirtebilirsiniz sistem bildirimleri için Hello cihaz halka ve/veya Titret, kampanya ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be148-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="be148-120">Bunun için toowork, toomake izni aşağıdaki hello bildirildiğinden emin olması (Merhaba sonra `</application>` etiketi):</span><span class="sxs-lookup"><span data-stu-id="be148-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="be148-121">Bu izin olmadan Android gösterildikten gelen sistem bildirimleri engeller, işaretlediyseniz hello halkası veya hello Titret hello Reach kampanya Yöneticisi'nde seçeneği.</span><span class="sxs-lookup"><span data-stu-id="be148-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="be148-122">Yerel gönderim</span><span class="sxs-lookup"><span data-stu-id="be148-122">Native Push</span></span>
<span data-ttu-id="be148-123">Reach modülünün yapılandırılmış, tooconfigure yerel gönderim toobe mümkün tooreceive hello Kampanyalar hello aygıtta gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="be148-124">Android iki hizmet destekliyoruz:</span><span class="sxs-lookup"><span data-stu-id="be148-124">We support two services on Android:</span></span>

* <span data-ttu-id="be148-125">Google Play aygıtları: kullanım [Google Cloud Messaging] aşağıdaki hello tarafından [nasıl tooIntegrate engagement GCM Kılavuzu](mobile-engagement-android-gcm-integrate.md) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="be148-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="be148-126">Amazon aygıtları: kullanım [Amazon Device Messaging] aşağıdaki hello tarafından [nasıl tooIntegrate engagement ADM Kılavuzu](mobile-engagement-android-adm-integrate.md) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="be148-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="be148-127">Tootarget istiyorsanız, Amazon ve Google Play aygıtlar, kendi olası toohave geliştirme için 1 AndroidManifest.xml/APK içindeki tüm öğeler.</span><span class="sxs-lookup"><span data-stu-id="be148-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="be148-128">Ancak GCM kod bulursanız tooAmazon gönderirken, bunlar uygulamanızı reddedebilir.</span><span class="sxs-lookup"><span data-stu-id="be148-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="be148-129">Bu durumda birden çok APKs kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="be148-130">**Hazır tooreceive ve görüntü Kampanyalar ulaşmak şimdi uygulamanızı değil!**</span><span class="sxs-lookup"><span data-stu-id="be148-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="be148-131">Nasıl toohandle veri gönderme</span><span class="sxs-lookup"><span data-stu-id="be148-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="be148-132">Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="be148-132">Integration</span></span>
<span data-ttu-id="be148-133">Uygulama toobe mümkün istiyorsanız tooreceive ulaşma veri iter, toocreate bir alt sınıfı olması `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` ve hello başvuru `AndroidManifest.xml` dosyası (Merhaba arasında `<application>` ve/veya `</application>` etiketleri):</span><span class="sxs-lookup"><span data-stu-id="be148-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="be148-134">Merhaba geçersiz kılabilirsiniz `onDataPushStringReceived` ve `onDataPushBase64Received` geri aramalar.</span><span class="sxs-lookup"><span data-stu-id="be148-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="be148-135">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="be148-135">Here is an example:</span></span>

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

### <a name="category"></a><span data-ttu-id="be148-136">Kategori</span><span class="sxs-lookup"><span data-stu-id="be148-136">Category</span></span>
<span data-ttu-id="be148-137">Merhaba kategori parametresi bir veri gönderme kampanya oluşturduğunuzda isteğe bağlıdır ve toofilter verileri iter sağlar.</span><span class="sxs-lookup"><span data-stu-id="be148-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="be148-138">Veri gönderimleri, farklı türlerde işleme birkaç yayın alıcılar varsa kullanışlıdır veya toopush değişik istiyorsanız, `Base64` veri ve istediğiniz tooidentify bunları ayrıştırma önce kendi türü.</span><span class="sxs-lookup"><span data-stu-id="be148-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="be148-139">Geri aramalar dönüş parametresi</span><span class="sxs-lookup"><span data-stu-id="be148-139">Callbacks' return parameter</span></span>
<span data-ttu-id="be148-140">Bazı yönergeler tooproperly tanıtıcı hello dönüş parametresi işte `onDataPushStringReceived` ve `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="be148-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="be148-141">Bir yayın alıcı döndürmelidir `null` içinde nasıl toohandle veri gönderme bilmiyorsa hello geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="be148-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="be148-142">Yayın Alıcınız hello veri gönderimi veya işlemelidir olup olmadığını hello kategori toodetermine kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="be148-143">Merhaba yayın alıcı birini döndürmelidir `true` içinde hello veri gönderimi kabul ederse hello geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="be148-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="be148-144">Merhaba yayın alıcı birini döndürmelidir `false` içinde hello veri gönderimi algılar ancak herhangi bir nedenle atar hello geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="be148-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="be148-145">Örneğin, sonuç `false` zaman hello alınan veri geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="be148-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="be148-146">Bir alıcı döndürür yayın varsa `true` başka döndürür while `false` hello aynı veri gönderimi, hello davranış tanımsızdır için hiçbir zaman, yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="be148-147">Merhaba dönüş türü yalnızca hello ulaşma istatistikleri için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="be148-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="be148-148">`Replied`Merhaba yayın alıcıları birini ya da döndürülürse artırılır `true` veya `false`.</span><span class="sxs-lookup"><span data-stu-id="be148-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="be148-149">`Actioned`yalnızca hello birini döndürülen alıcıları yayını olmazsa artırılır `true`.</span><span class="sxs-lookup"><span data-stu-id="be148-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="be148-150">Nasıl toocustomize Kampanyalar</span><span class="sxs-lookup"><span data-stu-id="be148-150">How toocustomize campaigns</span></span>
<span data-ttu-id="be148-151">toocustomize Kampanyalar hello Reach SDK sağlanan hello düzenleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be148-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="be148-152">Merhaba düzenleri kullanılan tüm hello tanımlayıcıları tutmak ve özellikle metin görünümleri ve görüntü görünümleri için bir tanımlayıcı kullanın hello görünüm hello türlerini tutmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="be148-153">Bazı görünümler yalnızca kullanılan toohide ya da kendi türü değiştirilemez alanları görüntüleyecek.</span><span class="sxs-lookup"><span data-stu-id="be148-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="be148-154">Sağlanan hello düzenleri toochange hello bir görünüm türünü düşünüyorsanız lütfen hello kaynak kodunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="be148-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="be148-155">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="be148-155">Notifications</span></span>
<span data-ttu-id="be148-156">Bildirimler iki tür vardır: farklı düzeni dosyaları kullanan sistem ve uygulama içi bildirimler.</span><span class="sxs-lookup"><span data-stu-id="be148-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="be148-157">Sistem bildirimleri</span><span class="sxs-lookup"><span data-stu-id="be148-157">System notifications</span></span>
<span data-ttu-id="be148-158">gereksinim duyduğunuz toouse hello toocustomize sistem bildirimleri **kategorileri**.</span><span class="sxs-lookup"><span data-stu-id="be148-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="be148-159">Çok atlayabilirsiniz[kategorileri](#categories).</span><span class="sxs-lookup"><span data-stu-id="be148-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="be148-160">Uygulama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="be148-160">In-app notifications</span></span>
<span data-ttu-id="be148-161">Varsayılan olarak, bir uygulama bildirimi dinamik olarak eklenen toohello geçerli etkinliği kullanıcı arabirimi teşekkürler toohello Android yöntemi görünümdür `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="be148-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="be148-162">Bu bildirim bir katmana çağrılır.</span><span class="sxs-lookup"><span data-stu-id="be148-162">This is called a notification overlay.</span></span> <span data-ttu-id="be148-163">Uygulamanız herhangi bir düzende, toomodify gerektirmediği için bildirim yer paylaşımları hızlı tümleştirme için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="be148-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="be148-164">bildirim yer paylaşımları hello görünümünü toomodify, yalnızca değiştirebileceğiniz hello dosya `engagement_notification_area.xml` tooyour gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="be148-165">Merhaba dosya `engagement_notification_overlay.xml` kullanılan toocreate olan bir bildirim katmana hello olduğu hello dosya içeren `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="be148-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="be148-166">Ayrıca toosuit özelleştirebilirsiniz gereksinimlerinizi (Merhaba bildirim alanında hello katmana içinde konumlandırma ettirilmesi gibi).</span><span class="sxs-lookup"><span data-stu-id="be148-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="be148-167">Bir etkinlik düzeni bir parçası olarak bildirim düzeni içerir</span><span class="sxs-lookup"><span data-stu-id="be148-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="be148-168">Yer paylaşımları hızlı tümleştirme için harika ancak kullanışsız veya özel durumlarda yan etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="be148-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="be148-169">Merhaba katmana sistem özel etkinlikler için kolay tooprevent yan etkileri kolaylaştırarak bir etkinlik düzeyde özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="be148-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="be148-170">Bizim bildirim düzeni tooinclude, varolan düzeni teşekkürler toohello içinde Android karar verebilirsiniz **dahil** deyimi.</span><span class="sxs-lookup"><span data-stu-id="be148-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="be148-171">Merhaba aşağıdaki değiştirilmiş bir örneğidir `ListActivity` düzenini yalnızca içeren bir `ListView`.</span><span class="sxs-lookup"><span data-stu-id="be148-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="be148-172">**Engagement tümleştirmesi önce:**</span><span class="sxs-lookup"><span data-stu-id="be148-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="be148-173">**Engagement tümleştirmesi sonra:**</span><span class="sxs-lookup"><span data-stu-id="be148-173">**After Engagement integration :**</span></span>

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

<span data-ttu-id="be148-174">Bu örnekte Hello özgün düzeni bir liste görünümü hello en üst düzey öğe kullanılan bu yana bir üst öğe kapsayıcısı eklediğimiz.</span><span class="sxs-lookup"><span data-stu-id="be148-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="be148-175">Ayrıca eklediğimiz `android:layout_weight="1"` bir liste görünümü aşağıda görünümü toobe mümkün tooadd yapılandırılmış `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="be148-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="be148-176">Merhaba Engagement Reach SDK hello bildirim düzenini bu etkinlikte bulunan ve bu etkinlik için bir katmana eklemez otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="be148-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="be148-177">Uygulamanızda bir ListActivity kullanırsanız, görünür bir Reach katmana, hello liste görünümünde tanımlandığında tooclicked öğeleri artık önler.</span><span class="sxs-lookup"><span data-stu-id="be148-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="be148-178">Bu bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="be148-178">This is a known issue.</span></span> <span data-ttu-id="be148-179">toowork bu soruna geçici, kendi listesi etkinlik düzeni gibi hello önceki örnekteki tooembed hello bildirim düzende öneririz.</span><span class="sxs-lookup"><span data-stu-id="be148-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="be148-180">Etkinlik başına uygulama bildirimini devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="be148-180">Disabling application notification per activity</span></span>
<span data-ttu-id="be148-181">Merhaba istemiyorsanız katmana toobe tooyour etkinlik eklendi ve kendi düzende hello bildirim düzeni eklemezseniz, bu etkinlik hello hello katmana devre dışı bırakabilir `AndroidManifest.xml` ekleyerek bir `meta-data` bölüm hello aşağıdakileri ister Örnek:</span><span class="sxs-lookup"><span data-stu-id="be148-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="be148-182"><a name="categories"></a>Kategorileri</span><span class="sxs-lookup"><span data-stu-id="be148-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="be148-183">Düzenleri sağlanan hello değiştirdiğinizde, tüm bildirimlerinizi hello görünümünü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="be148-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="be148-184">Çeşitli hedeflenen toodefine (büyük olasılıkla davranışları) bildirimleri için görünür kategoriler.</span><span class="sxs-lookup"><span data-stu-id="be148-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="be148-185">Bir kategori Reach kampanya oluşturduğunuzda belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="be148-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="be148-186">Bu belgenin sonraki bölümlerinde açıklanan kategoriler de duyuruları ve yoklamaları, özelleştirmenize olanak tanır olduğunu aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="be148-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="be148-187">Merhaba uygulaması başlatıldığında tooregister bildirimlerinizi için bir kategori işleyici, tooadd bir çağrı gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be148-188">Merhaba uyarı hello android: işlem özniteliği hakkında okuyun \<android sdk katılım işlem\> hello içinde nasıl tooIntegrate katılım devam etmeden önce Android konuda.</span><span class="sxs-lookup"><span data-stu-id="be148-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="be148-189">Merhaba aşağıdaki örneği hello önceki uyarı onaylanır ve bir alt sınıfı kullanma varsayar `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="be148-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

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

<span data-ttu-id="be148-190">Merhaba `MyNotifier` nesne uygulamasıdır hello hello bildirim kategori işleyici.</span><span class="sxs-lookup"><span data-stu-id="be148-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="be148-191">Her iki hello uygulaması olan `EngagementNotifier` arabirimi veya hello varsayılan uygulaması bir alt sınıfı: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="be148-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="be148-192">Aynı bildirim hello Not birkaç kategorisi işleyebilir, bunları şu şekilde kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be148-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="be148-193">tooreplace hello varsayılan kategori uygulaması, aşağıdaki örneğine hello uygulamanızı gibi kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be148-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

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

<span data-ttu-id="be148-194">işleyici kullanılan hello geçerli kategorisi çoğu yöntemleri içinde geçersiz parametre olarak geçirilen `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="be148-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="be148-195">Olarak ya da geçirilir bir `String` parametresi veya dolaylı bir `EngagementReachContent` olan nesne bir `getCategory()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="be148-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="be148-196">Üzerinde yöntemleri tanımlayarak hello bildirim oluşturma işlemi çoğunu değiştirebilirsiniz `EngagementDefaultNotifier`, daha gelişmiş özelleştirme eşitleyerek için ücretsiz tootake hello teknik belgeler ve hello kaynak koduna bakın.</span><span class="sxs-lookup"><span data-stu-id="be148-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="be148-197">Uygulama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="be148-197">In-app notifications</span></span>
<span data-ttu-id="be148-198">Belirli bir kategorideki için yalnızca toouse alternatif düzenleri istiyorsanız, bu örnek aşağıdaki hello olduğu gibi uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be148-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

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

<span data-ttu-id="be148-199">**Örnek `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="be148-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="be148-200">Gördüğünüz gibi hello katmana görünüm tanımlayıcısı hello standart bir farklıdır.</span><span class="sxs-lookup"><span data-stu-id="be148-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="be148-201">Her düzeni yer paylaşımları için benzersiz bir tanımlayıcı kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="be148-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="be148-202">**Örnek `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="be148-202">**Example of `my_notification_area.xml` :**</span></span>

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

<span data-ttu-id="be148-203">Gördüğünüz gibi hello bildirim alanı görünüm tanımlayıcısı hello standart bir farklıdır.</span><span class="sxs-lookup"><span data-stu-id="be148-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="be148-204">Her düzeni bildirim alanları için benzersiz bir tanımlayıcı kullanır önemlidir.</span><span class="sxs-lookup"><span data-stu-id="be148-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="be148-205">Bu basit örnek kategorisinin Merhaba ekranında hello üst kısmında gösterilen uygulama (veya uygulama) bildirim yapar.</span><span class="sxs-lookup"><span data-stu-id="be148-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="be148-206">Merhaba bildirim alanında kendisini kullanılan hello standart tanımlayıcıları değişmemiştir.</span><span class="sxs-lookup"><span data-stu-id="be148-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="be148-207">Tooredefine hello sahip, toochange istiyorsanız `EngagementDefaultNotifier.prepareInAppArea` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="be148-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="be148-208">Önerilir toolook hello teknik belgeler ve hello kaynak kodunu `EngagementNotifier` ve `EngagementDefaultNotifier` bu Gelişmiş özelleştirme düzeyi istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="be148-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="be148-209">Sistem bildirimleri</span><span class="sxs-lookup"><span data-stu-id="be148-209">System notifications</span></span>
<span data-ttu-id="be148-210">Genişletme tarafından `EngagementDefaultNotifier`, geçersiz kılabilirsiniz `onNotificationPrepared` hello varsayılan uygulaması tarafından hazırlanan tooalter hello bildirim.</span><span class="sxs-lookup"><span data-stu-id="be148-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="be148-211">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="be148-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="be148-212">Bu örnek hello "devam eden" kategorisi kullanıldığında, devam eden bir olay görüntülenmesini içerik için bir sistem bildirimi yapar.</span><span class="sxs-lookup"><span data-stu-id="be148-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="be148-213">Toobuild hello istiyorsanız `Notification` nesne baştan geri dönebilirsiniz `false` toohello yöntemi ve çağrı `notify` kendiniz hello `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="be148-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="be148-214">Bu durumda, tutmanızı önemli bir `contentIntent`, `deleteIntent` ve bildirim tanımlayıcısı tarafından kullanılan hello `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="be148-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="be148-215">Bu tür bir uygulama doğru bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="be148-215">Here is a correct example of such an implementation:</span></span>

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
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="be148-216">Yalnızca bildirim duyuruları</span><span class="sxs-lookup"><span data-stu-id="be148-216">Notification only announcements</span></span>
<span data-ttu-id="be148-217">Merhaba hello yönetimini tıklayın yalnızca duyuru kılarak özelleştirilebilir bir bildirim `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hazırlanmış toomodify hello `Intent`.</span><span class="sxs-lookup"><span data-stu-id="be148-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="be148-218">Bu yöntemi kullanarak tootune hello bayrakları kolayca sağlar.</span><span class="sxs-lookup"><span data-stu-id="be148-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="be148-219">Örneğin tooadd hello `SINGLE_TOP` bayrağı:</span><span class="sxs-lookup"><span data-stu-id="be148-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="be148-220">Bu yöntem, eylem URL'si olmadan duyuru kullanılarak çağrılamaz. böylece arka planda ise, sistem bildirimleri eylemi olmadan URL şimdi hello uygulama başlatma eski katılım kullanıcılar için lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="be148-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="be148-221">Hello hedefi özelleştirirken düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="be148-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="be148-222">Ayrıca uygulayabilirsiniz `EngagementNotifier.executeNotifAnnouncementAction` sıfırdan.</span><span class="sxs-lookup"><span data-stu-id="be148-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="be148-223">Bildirim yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="be148-223">Notification life cycle</span></span>
<span data-ttu-id="be148-224">Merhaba varsayılan kategori kullanırken, bazı yaşam döngüsü yöntemleri üzerinde hello denir `EngagementReachInteractiveContent` nesne tooreport istatistikleri ve güncelleştirme hello kampanya durumu:</span><span class="sxs-lookup"><span data-stu-id="be148-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="be148-225">Merhaba bildirim uygulamada görüntülenen ya da hello durum çubuğunda put hello `displayNotification` yöntemi (hangi istatistikleri raporları) çağrılır tarafından `EngagementReachAgent` varsa `handleNotification` döndürür `true`.</span><span class="sxs-lookup"><span data-stu-id="be148-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="be148-226">Merhaba bildirim kapatıldığında, hello `exitNotification` yöntemi çağrıldığında, istatistik bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="be148-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="be148-227">Merhaba bildirim tıkladıysanız `actionNotification` olduğu adlı istatistik bildirilir ve ilişkili hello hedefi başlatıldığında.</span><span class="sxs-lookup"><span data-stu-id="be148-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="be148-228">Uygulamanıza `EngagementNotifier` atlamaların hello varsayılan davranışı, toocall bu yaşam döngüsü yöntemleri başınıza gerekir.</span><span class="sxs-lookup"><span data-stu-id="be148-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="be148-229">Örnek hello hello varsayılan davranışı burada atlanır bazı durumlarda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="be148-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="be148-230">Genişletme yok `EngagementDefaultNotifier`, sıfırdan kategori işleme uygulanan örn.</span><span class="sxs-lookup"><span data-stu-id="be148-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="be148-231">Sistem bildirimleri için hello geçersiz kılınmış `onNotificationPrepared` ve değiştirdiğiniz `contentIntent` veya `deleteIntent` hello içinde `Notification` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="be148-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="be148-232">Uygulama bildirimleri için geçersiz kılınmış `prepareInAppArea`emin toomap olması en az `actionNotification` U.I denetimlerin tooone.</span><span class="sxs-lookup"><span data-stu-id="be148-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="be148-233">Varsa `handleNotification` bir özel durum, içerik hello silinir ve `dropContent` olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="be148-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="be148-234">Bu durum istatistiklerine bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="be148-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="be148-235">Duyuruları ve yoklamaları</span><span class="sxs-lookup"><span data-stu-id="be148-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="be148-236">Düzenleri</span><span class="sxs-lookup"><span data-stu-id="be148-236">Layouts</span></span>
<span data-ttu-id="be148-237">Merhaba değiştirebileceğiniz `engagement_text_announcement.xml`, `engagement_web_announcement.xml` ve `engagement_poll.xml` toocustomize metin Duyurular, web duyuruları ve yoklamaları dosyaları.</span><span class="sxs-lookup"><span data-stu-id="be148-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="be148-238">Bu dosyalar hello başlık alanı ve hello düğme alanının için iki ortak düzenleri paylaşır.</span><span class="sxs-lookup"><span data-stu-id="be148-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="be148-239">Merhaba düzeni hello başlık `engagement_content_title.xml` ve kullandığı hello hello arka plan için eponymous drawable dosyası.</span><span class="sxs-lookup"><span data-stu-id="be148-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="be148-240">Merhaba hello eylem ve çıkış düğmeleri için Düzen olan `engagement_button_bar.xml` ve kullandığı hello hello arka plan için eponymous drawable dosyası.</span><span class="sxs-lookup"><span data-stu-id="be148-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="be148-241">Bir yoklamada soru düzeni hello ve seçimleri birkaç kez hello kullanarak dinamik olarak şişirileceğini `engagement_question.xml` düzeni dosyasını hello sorularınız ve hello `engagement_choice.xml` hello seçimler dosya.</span><span class="sxs-lookup"><span data-stu-id="be148-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="be148-242">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="be148-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="be148-243">Alternatif düzenleri</span><span class="sxs-lookup"><span data-stu-id="be148-243">Alternate layouts</span></span>
<span data-ttu-id="be148-244">Bildirimler gibi hello kampanya kategori duyuruları ve yoklamaları için kullanılan toohave alternatif düzenleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="be148-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="be148-245">Örneğin, bir metin duyuru için bir kategori toocreate genişletebilirsiniz `EngagementTextAnnouncementActivity` ve hello başvuru `AndroidManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="be148-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="be148-246">Merhaba hedefi hello kategoriye Not filtre kullanılır toomake hello farkı hello varsayılan duyuru etkinlik.</span><span class="sxs-lookup"><span data-stu-id="be148-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="be148-247">Hello SDK ulaşmak için belirli bir kategorideki hello hedefi sistem tooresolve hello sağ etkinliğini kullanır ve hello çözümlemesi başarısız olursa, geri hello varsayılan kategorisine göre döner.</span><span class="sxs-lookup"><span data-stu-id="be148-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="be148-248">Tooimplement sahip `MyCustomTextAnnouncementActivity`, yalnızca toochange hello düzeni istediğiniz (ancak aynı tanımlayıcılarını görüntüle hello tutmak varsa), yalnızca toodefine hello sınıfı gibi aşağıdaki örneğine hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="be148-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="be148-249">yalnızca metin Duyurular, tooreplace hello varsayılan kategorisini değiştirin `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` , uygulamanız tarafından.</span><span class="sxs-lookup"><span data-stu-id="be148-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="be148-250">Web duyuruları ve yoklamaları için benzer bir şekilde özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="be148-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="be148-251">Web duyuruları için genişletebilirsiniz `EngagementWebAnnouncementActivity` ve hello etkinlik bildirmek `AndroidManifest.xml` aşağıdaki örneğine hello ister:</span><span class="sxs-lookup"><span data-stu-id="be148-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="be148-252">Anketler için genişletebilirsiniz `EngagementPollActivity` ve içinde hello bildirme `AndroidManifest.xml` aşağıdaki örneğine hello ister:</span><span class="sxs-lookup"><span data-stu-id="be148-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="be148-253">Sıfırdan uygulama</span><span class="sxs-lookup"><span data-stu-id="be148-253">Implementation from scratch</span></span>
<span data-ttu-id="be148-254">Hello genişletmeden kategorileri duyuru (ve yoklama) etkinliklerinizi için uygulayabileceğiniz `Engagement*Activity` sınıflar tarafından sağlanan hello Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="be148-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="be148-255">Bu örneğin toodefine görünümlerini aynı hello hello standart düzenleri kullanmaz bir düzen istiyorsanız kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="be148-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="be148-256">Gibi gelişmiş bildirim özelleştirmesi hello kaynak koduna hello standart uygulama toolook önerilir.</span><span class="sxs-lookup"><span data-stu-id="be148-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="be148-257">Göz önünde bazı şeyleri tookeep şunlardır: ulaşma hello içerik tanıtıcısı olan bir ek parametre hello etkinliği belirli bir amaç (karşılık gelen toohello hedefi Filtresi) ile başlar.</span><span class="sxs-lookup"><span data-stu-id="be148-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="be148-258">ne zaman hello oluşturma kampanya hello web sitesinde, belirtilen hello alanları içeren tooretrieve hello içerik nesnesini bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be148-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

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

<span data-ttu-id="be148-259">STATISTICS için hello içerik hello görüntülenen bildirmelisiniz `onResume` olay:</span><span class="sxs-lookup"><span data-stu-id="be148-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="be148-260">Ardından, toocall ya da unutmayın `actionContent(this)` veya `exitContent(this)` arka plana hello etkinlik geçmeden önce hello içerik nesne üzerinde.</span><span class="sxs-lookup"><span data-stu-id="be148-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="be148-261">Ya da yok çağırırsanız `actionContent` veya `exitContent`, istatistikleri (yani hello kampanyası hiçbir analytics) gönderilen olmaz ve daha da önemlisi, hello sonraki kampanyalar, değil hello uygulama işlemini yeniden başlatılana kadar bildirilir.</span><span class="sxs-lookup"><span data-stu-id="be148-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="be148-262">Yönlendirme veya başka yapılandırma değişiklikleri veya arka plana hello etkinliğine gittiği olup olmadığını hello kod hassas toodetermine olun, standart uygulama yapar emin hello içerik hello kullanıcı hello etkinlik (ya da bırakırsa çıktı olarak bildirilen hello tuşuna basarak `HOME` veya `BACK`) ancak hello yönlendirmesini değişirse değil.</span><span class="sxs-lookup"><span data-stu-id="be148-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="be148-263">Merhaba ilginç parçası hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="be148-263">Here is hello interesting part of hello implementation:</span></span>

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
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="be148-264">Aradığınız varsa, gördüğünüz gibi `actionContent(this)` hello Etkinliğin bitiş sonra `exitContent(this)` herhangi bir etkisi olmadan güvenli bir şekilde çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="be148-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
