---
title: "Azure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="4bfa8-103">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="4bfa8-103">Upgrade procedures</span></span>
<span data-ttu-id="4bfa8-104">Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz, SDK'yı yükseltirken aşağıdaki noktaları dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="4bfa8-105">SDK çeşitli sürümleri eksik, birçok yordamı uygulamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="4bfa8-106">Örneğin, 1.4.0 önce "Kimden 1.4.0 1.5.0 için" yordamını takip etmek için sahip 1.6.0 sonra "Kimden 1.5.0 1.6.0 için" yordamı geçiş ise.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="4bfa8-107">Yükseltme, seçtiğiniz sürüm değiştirmek zorunda `mobile-engagement-VERSION.jar` yeni bir.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="4bfa8-108">4.2.0 4.2.1 için</span><span class="sxs-lookup"><span data-stu-id="4bfa8-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="4bfa8-109">Bu adım SDK'ın herhangi bir sürümü üzerinde gerçekte yapılabilir, ulaşma etkinlikleri tümleştirdiğinizde güvenlik geliştirme olur.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="4bfa8-110">Şimdi eklemelisiniz `exported="false"` tüm ulaşma etkinliklere.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="4bfa8-111">Reach etkinlikleri şimdi şöyle görünmelidir, `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-to-410"></a><span data-ttu-id="4bfa8-112">4.0.0 4.1.0'da için</span><span class="sxs-lookup"><span data-stu-id="4bfa8-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="4bfa8-113">SDK şimdi tanıtıcı yeni izni modelden Android M.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="4bfa8-114">Konum özelliklerini kullanmak veya büyük resmi bildirimleri okuyun [Bu bölümde](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="4bfa8-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="4bfa8-115">Yeni izni model ek olarak, çalışma zamanında yapılandırma konumu özellikleri artık desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="4bfa8-116">Biz yine bildirimi parametreleri konumu için uyumludur, ancak artık kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="4bfa8-117">Çalışma zamanı yapılandırmasını kullanmak için aşağıdaki bölümlerden kaldırın, ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="4bfa8-118">okuyup [bu güncelleştirilmiş yordamı](mobile-engagement-android-integrate-engagement.md#location-reporting) çalışma zamanı yapılandırma kullanmayı.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="4bfa8-119">3.0.0 4.0.0 için</span><span class="sxs-lookup"><span data-stu-id="4bfa8-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="4bfa8-120">Yerel gönderim</span><span class="sxs-lookup"><span data-stu-id="4bfa8-120">Native push</span></span>
<span data-ttu-id="4bfa8-121">İtme kampanya herhangi bir türde yerel gönderim kimlik bilgilerini yapılandırmak için yerel gönderim (GCM/ADM) şimdi de için uygulama içi Bildirimlerde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="4bfa8-122">Aksi halde zaten Lütfen izleyin [bu yordamı](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="4bfa8-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="4bfa8-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4bfa8-123">AndroidManifest.xml</span></span>
<span data-ttu-id="4bfa8-124">Reach tümleştirme değiştirildi ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="4bfa8-125">Bu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="4bfa8-126">Tarafından</span><span class="sxs-lookup"><span data-stu-id="4bfa8-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
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

<span data-ttu-id="4bfa8-127">Yapıldığında büyük olasılıkla yükleme ekran şimdi duyuru (metin/web içerik ile) ya da bir yoklama tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="4bfa8-128">Bu 4.0.0 içinde çalışmak bu kampanyalar için eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="4bfa8-129">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4bfa8-129">Resources</span></span>
<span data-ttu-id="4bfa8-130">Yeni katıştırmak `res/layout/engagement_loading.xml` projenize dosya.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="4bfa8-131">2.4.0 3.0.0 için</span><span class="sxs-lookup"><span data-stu-id="4bfa8-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="4bfa8-132">Aşağıdaki nasıl Azure Mobile Engagement tarafından desteklenen bir uygulamaya Capptain SAS tarafından sunulan Capptain hizmetinden bir SDK tümleştirmesi geçirileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="4bfa8-133">Önceki bir sürümünden geçiş yapıyorsanız, lütfen 2.4.0 için ilk geçirmek için Capptain web sitesine başvurun ve sonra aşağıdaki yordamı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bfa8-134">Capptain ve Mobile Engagement aynı Hizmetleri değildir ve aşağıda verilen yordamı yalnızca istemci uygulaması geçirmek nasıl vurgular.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="4bfa8-135">Uygulama SDK'yı geçirme verilerinizi Capptain sunucularından Mobile Engagement sunucuya geçişi YAPILMAZ.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="4bfa8-136">JAR dosyasını</span><span class="sxs-lookup"><span data-stu-id="4bfa8-136">JAR file</span></span>
<span data-ttu-id="4bfa8-137">Değiştir `capptain.jar` tarafından `mobile-engagement-VERSION.jar` içinde `libs` klasörü.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="4bfa8-138">Kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="4bfa8-138">Resource files</span></span>
<span data-ttu-id="4bfa8-139">Bizim sağladığımız her kaynak dosyası (önüne `capptain_`) yenilerini tarafından değiştirilmesi gereken (önekine sahip `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="4bfa8-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="4bfa8-140">Bu dosyaları özelleştirdiyseniz, özelleştirme yeni dosyalarda yeniden uygulamak sahip **kaynak dosyalarında tüm tanımlayıcıları da yeniden adlandırıldığı**.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="4bfa8-141">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="4bfa8-141">Application ID</span></span>
<span data-ttu-id="4bfa8-142">Şimdi Engagement SDK'sı tanımlayıcıları uygulama tanımlayıcısı gibi yapılandırmak için bir bağlantı dizesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="4bfa8-143">Kullanmak zorunda `EngagementAgent.init` Başlatıcısı etkinliklerinizi şöyle yöntemi:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="4bfa8-144">Bağlantı dizesi, uygulamanız için Azure portalında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="4bfa8-145">Lütfen herhangi çağrısına kaldırın `CapptainAgent.configure` olarak `EngagementAgent.init` o yöntemi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="4bfa8-146">`appId` Artık kullanılarak yapılandırılabilir `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="4bfa8-147">Lütfen bu bölümünden kaldırın, `AndroidManifest.xml` , varsa:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="4bfa8-148">Java API’si</span><span class="sxs-lookup"><span data-stu-id="4bfa8-148">Java API</span></span>
<span data-ttu-id="4bfa8-149">Yeniden adlandırılacak her çağrı için herhangi bir Java sınıf bizim SDK'sının sahiptir; Örneğin, `CapptainAgent.getInstance(this)` kaydedilmelidir `EngagementAgent.getInstance(this)`, `extends CapptainActivity` kaydedilmelidir `extends EngagementActivity` vb....</span><span class="sxs-lookup"><span data-stu-id="4bfa8-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="4bfa8-150">Varsayılan aracı tercih dosyalarını ile tümleşik varsayılan dosya adı şimdi varsa, `engagement.agent` ve anahtar `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="4bfa8-151">Web duyuruları oluştururken, Javascript bağlayıcı sunulmuştur `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="4bfa8-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4bfa8-152">AndroidManifest.xml</span></span>
<span data-ttu-id="4bfa8-153">Çok sayıda değişiklik vardır oldu, hizmet artık paylaşılmayan ve alıcıları çok değildir verilebilir artık.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="4bfa8-154">Hizmet bildirimi artık daha kolaydır; hedefi filtre ve içindeki tüm meta veri kaldırıp eklemek `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="4bfa8-155">Ayrıca her şeyi engagement kullanılacağı adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="4bfa8-156">Şimdi gibi görünüyor:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="4bfa8-157">Test günlüklerinin sağlamak istiyorsanız, meta verileri artık uygulama etiketi taşındı ve yeniden adlandırıldı:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="4bfa8-158">Tüm diğer meta verileri yalnızca yeniden adlandırıldığı, tam listesini (indirmelere rename yalnızca kullandığınız olanlar) aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="4bfa8-159">Bu değişikliği kaldırmak zorunda SDK Google Play ve izleme SmartAd kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="4bfa8-160">Reach etkinlikleri şöyle bildirilir:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-160">The Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="4bfa8-161">Özel erişim etkinlikler varsa, ya da eşleşecek şekilde hedefi eylemleri yalnızca değiştirmeye ihtiyaç `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` veya `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="4bfa8-162">Yayın alıcıları yeniden adlandırıldığı artı şimdi eklediğimiz `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="4bfa8-163">Yeni belirtimi, (indirmelere rename yalnızca kullandığınız olanlar) alıcılarla tam listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="4bfa8-164">Bu bölümde kaldırmanız gerekir böylece alıcı izleme kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="4bfa8-165">Unutmayın yayın alıcı uygulanmasını bildirimi **EngagementMessageReceiver** deki `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="4bfa8-166">Göndermek ve rasgele XMPP iletileri rasgele XMPP varlıklardan kaldırmak için API ve cihazlar arasında ileti gönderme ve alma için API kaldırılmış olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="4bfa8-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="4bfa8-167">Böylece, aşağıdaki geri çağırmaları gelen silmek de, **EngagementMessageReceiver** uygulama:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="4bfa8-168">ve</span><span class="sxs-lookup"><span data-stu-id="4bfa8-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="4bfa8-169">üzerinde herhangi bir çağrısına silme **EngagementAgent** için:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="4bfa8-170">ve</span><span class="sxs-lookup"><span data-stu-id="4bfa8-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="4bfa8-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="4bfa8-171">Proguard</span></span>
<span data-ttu-id="4bfa8-172">Proguard yapılandırma rebranding tarafından etkilenebilir, kuralları şimdi gibi arıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="4bfa8-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

