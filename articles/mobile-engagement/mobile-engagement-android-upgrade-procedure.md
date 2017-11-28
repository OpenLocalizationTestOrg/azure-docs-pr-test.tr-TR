---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
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
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="987e5-103">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="987e5-103">Upgrade procedures</span></span>
<span data-ttu-id="987e5-104">Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.</span><span class="sxs-lookup"><span data-stu-id="987e5-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="987e5-105">Merhaba SDK çeşitli sürümleri eksik birkaç yordamları toofollow olabilir.</span><span class="sxs-lookup"><span data-stu-id="987e5-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="987e5-106">1.4.0 geçirirseniz örneğin hello izleyin toofirst sahip too1.6.0 "1.4.0 gelen too1.5.0" yordamı sonra hello "1.5.0 gelen too1.6.0" yordamı.</span><span class="sxs-lookup"><span data-stu-id="987e5-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="987e5-107">Yükseltme, seçtiğiniz hello sürüm tooreplace hello sahip `mobile-engagement-VERSION.jar` hello yeni bir tane ile.</span><span class="sxs-lookup"><span data-stu-id="987e5-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="987e5-108">4.2.0 gelen too4.2.1</span><span class="sxs-lookup"><span data-stu-id="987e5-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="987e5-109">Bu adım gerçekte herhangi bir hello SDK sürümünde yapılabilir, ulaşma etkinlikleri tümleştirdiğinizde güvenlik geliştirme olur.</span><span class="sxs-lookup"><span data-stu-id="987e5-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="987e5-110">Şimdi eklemelisiniz `exported="false"` tooall ulaşma etkinlikler.</span><span class="sxs-lookup"><span data-stu-id="987e5-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="987e5-111">Reach etkinlikleri şimdi şöyle görünmelidir, `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="987e5-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-too410"></a><span data-ttu-id="987e5-112">4.0.0 gelen too4.1.0</span><span class="sxs-lookup"><span data-stu-id="987e5-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="987e5-113">Merhaba SDK şimdi tanıtıcı yeni izni modelden Android M.</span><span class="sxs-lookup"><span data-stu-id="987e5-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="987e5-114">Konum özelliklerini kullanmak veya büyük resmi bildirimleri okuyun [Bu bölümde](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="987e5-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="987e5-115">Ayrıca toohello yeni izni modeli şimdi konum özelliklerini çalışma zamanında yapılandırma destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="987e5-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="987e5-116">Biz yine hello bildirimi parametreleri konumu için uyumludur, ancak artık kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="987e5-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="987e5-117">Kaldır hello aşağıdaki toouse çalışma zamanı yapılandırması, bölümler, ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="987e5-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="987e5-118">okuyup [bu güncelleştirilmiş yordamı](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse çalışma zamanı yapılandırma yerine.</span><span class="sxs-lookup"><span data-stu-id="987e5-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="987e5-119">3.0.0 gelen too4.0.0</span><span class="sxs-lookup"><span data-stu-id="987e5-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="987e5-120">Yerel gönderim</span><span class="sxs-lookup"><span data-stu-id="987e5-120">Native push</span></span>
<span data-ttu-id="987e5-121">İtme kampanya herhangi bir türde hello yerel gönderim kimlik bilgilerini yapılandırmak için yerel gönderim (GCM/ADM) şimdi de için uygulama içi Bildirimlerde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="987e5-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="987e5-122">Aksi halde zaten Lütfen izleyin [bu yordamı](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="987e5-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="987e5-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="987e5-123">AndroidManifest.xml</span></span>
<span data-ttu-id="987e5-124">Reach tümleştirme değiştirildi ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="987e5-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="987e5-125">Bu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="987e5-125">Replace this:</span></span>

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

<span data-ttu-id="987e5-126">Tarafından</span><span class="sxs-lookup"><span data-stu-id="987e5-126">By</span></span>

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

<span data-ttu-id="987e5-127">Yapıldığında büyük olasılıkla yükleme ekran şimdi duyuru (metin/web içerik ile) ya da bir yoklama tıklatın.</span><span class="sxs-lookup"><span data-stu-id="987e5-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="987e5-128">Tooadd bu bu Kampanyalar toowork 4.0.0 içinde olan:</span><span class="sxs-lookup"><span data-stu-id="987e5-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="987e5-129">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="987e5-129">Resources</span></span>
<span data-ttu-id="987e5-130">Merhaba yeni katıştırmak `res/layout/engagement_loading.xml` projenize dosya.</span><span class="sxs-lookup"><span data-stu-id="987e5-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="987e5-131">2.4.0 gelen too3.0.0</span><span class="sxs-lookup"><span data-stu-id="987e5-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="987e5-132">Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="987e5-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="987e5-133">Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too2.4.0 ilk bakın ve hello aşağıdaki yordamı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="987e5-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="987e5-134">Capptain ve Mobile Engagement değil hello aynı hizmetler ve nasıl toomigrate hello istemci uygulamasını yalnızca vurgular verilen yordamı hello.</span><span class="sxs-lookup"><span data-stu-id="987e5-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="987e5-135">Geçirme hello SDK hello uygulama verilerinizi hello Capptain sunucuları toohello Mobile Engagement sunucularından geçişi YAPILMAZ.</span><span class="sxs-lookup"><span data-stu-id="987e5-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="987e5-136">JAR dosyasını</span><span class="sxs-lookup"><span data-stu-id="987e5-136">JAR file</span></span>
<span data-ttu-id="987e5-137">Değiştir `capptain.jar` tarafından `mobile-engagement-VERSION.jar` içinde `libs` klasörü.</span><span class="sxs-lookup"><span data-stu-id="987e5-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="987e5-138">Kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="987e5-138">Resource files</span></span>
<span data-ttu-id="987e5-139">Bizim sağladığımız her kaynak dosyası (önüne `capptain_`) sahip toobe yerine yenilerini hello tarafından (önekine sahip `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="987e5-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="987e5-140">Bu dosyaları özelleştirdiyseniz, toore sahip-özelleştirme hello yeni dosyalarda uygulamak **hello kaynak dosyalarında tüm hello tanımlayıcıları da yeniden adlandırıldığı**.</span><span class="sxs-lookup"><span data-stu-id="987e5-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="987e5-141">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="987e5-141">Application ID</span></span>
<span data-ttu-id="987e5-142">Şimdi katılım bir bağlantı dizesi tooconfigure hello SDK tanımlayıcıları hello uygulama tanımlayıcısı gibi kullanır.</span><span class="sxs-lookup"><span data-stu-id="987e5-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="987e5-143">Toouse sahip `EngagementAgent.init` Başlatıcısı etkinliklerinizi şöyle yöntemi:</span><span class="sxs-lookup"><span data-stu-id="987e5-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="987e5-144">Merhaba bağlantı dizesi, uygulamanız için Azure portalında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="987e5-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="987e5-145">Lütfen herhangi bir çağrısına çok kaldırın`CapptainAgent.configure` olarak `EngagementAgent.init` o yöntemi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="987e5-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="987e5-146">Merhaba `appId` artık kullanılarak yapılandırılabilir `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="987e5-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="987e5-147">Lütfen bu bölümünden kaldırın, `AndroidManifest.xml` , varsa:</span><span class="sxs-lookup"><span data-stu-id="987e5-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="987e5-148">Java API’si</span><span class="sxs-lookup"><span data-stu-id="987e5-148">Java API</span></span>
<span data-ttu-id="987e5-149">Her çağrı tooany Java sınıfı bizim SDK'sının yeniden adlandırılmış toobe; yine de sahip istiyor musunuz? Örneğin, `CapptainAgent.getInstance(this)` kaydedilmelidir `EngagementAgent.getInstance(this)`, `extends CapptainActivity` kaydedilmelidir `extends EngagementActivity` vb....</span><span class="sxs-lookup"><span data-stu-id="987e5-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="987e5-150">Varsayılan aracı tercih dosyalarını ile tümleşik hello varsayılan dosya adı şimdi varsa, `engagement.agent` ve başlangıç anahtarı `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="987e5-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="987e5-151">Web duyuruları oluştururken hello Javascript bağlayıcı sunulmuştur `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="987e5-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="987e5-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="987e5-152">AndroidManifest.xml</span></span>
<span data-ttu-id="987e5-153">Çok sayıda değişiklik vardır oldu, hello hizmeti artık paylaşılmayan ve alıcıları çok değildir verilebilir artık.</span><span class="sxs-lookup"><span data-stu-id="987e5-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="987e5-154">Merhaba hizmet bildirimi artık daha kolaydır; Merhaba hedefi filtre ve içindeki tüm meta veri kaldırıp eklemek `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="987e5-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="987e5-155">Ayrıca, yeniden adlandırılmış toouse katılım gereken her şey vardır.</span><span class="sxs-lookup"><span data-stu-id="987e5-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="987e5-156">Şimdi gibi görünüyor:</span><span class="sxs-lookup"><span data-stu-id="987e5-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="987e5-157">Tooenable test günlüklerinin istediğinizde hello meta verileri artık bırakıldı toohello uygulama etiketi taşınır ve yeniden adlandırıldı:</span><span class="sxs-lookup"><span data-stu-id="987e5-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="987e5-158">Tüm diğer meta verileri yalnızca yeniden adlandırıldığı, hello tam listesi (kullandığınız Elbette yeniden adlandırma yalnızca hello olanlar) aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="987e5-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="987e5-159">Google Play ve SmartAd izleme kaldırıldı SDK'dan yalnızca tooremove bu değişikliği gerekir:</span><span class="sxs-lookup"><span data-stu-id="987e5-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="987e5-160">Merhaba ulaşma etkinlikleri şöyle bildirilir:</span><span class="sxs-lookup"><span data-stu-id="987e5-160">hello Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="987e5-161">Özel erişim etkinlikler varsa, yalnızca toochange hello hedefi Eylemler toomatch ya da ihtiyacınız `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` veya `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="987e5-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="987e5-162">Merhaba yayın alıcıları yeniden adlandırıldığı artı şimdi eklediğimiz `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="987e5-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="987e5-163">Merhaba yeni belirtimi (kullandığınız Elbette yeniden adlandırma yalnızca hello olanlar) hello alıcılarla hello tam listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="987e5-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="987e5-164">Bu bölümde tooremove alacak şekilde alıcı izleme kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="987e5-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="987e5-165">Uygulamanıza hello Hello bildirimi alıcı yayın Not **EngagementMessageReceiver** hello değişti `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="987e5-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="987e5-166">Bu hello API toosend ekleme ve kaldırma rasgele XMPP rasgele XMPP varlıklardan iletileri olduğundan ve API toosend hello ve cihazlar arasında iletilerini kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="987e5-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="987e5-167">Ayrıca bu nedenle, gelen geri aramalar aşağıdaki toodelete hello vardır, **EngagementMessageReceiver** uygulama:</span><span class="sxs-lookup"><span data-stu-id="987e5-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="987e5-168">ve</span><span class="sxs-lookup"><span data-stu-id="987e5-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="987e5-169">üzerinde herhangi bir çağrısına silme **EngagementAgent** için:</span><span class="sxs-lookup"><span data-stu-id="987e5-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="987e5-170">ve</span><span class="sxs-lookup"><span data-stu-id="987e5-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="987e5-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="987e5-171">Proguard</span></span>
<span data-ttu-id="987e5-172">Proguard yapılandırma rebranding, kuralları şimdi gibi aradığınız hello tarafından etkilenebilir:</span><span class="sxs-lookup"><span data-stu-id="987e5-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

