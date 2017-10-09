---
title: "Azure Mobile Engagement Android SDK aaaAdvanced yapılandırma"
description: "Gelişmiş yapılandırma seçenekleri Hello Azure Mobile Engagement Android SDK'sı Android derleme bildirimi de dahil olmak üzere hello açıklar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="b8579-103">Gelişmiş yapılandırma için Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="b8579-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8579-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="b8579-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="b8579-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b8579-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="b8579-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b8579-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="b8579-107">Android</span><span class="sxs-lookup"><span data-stu-id="b8579-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="b8579-108">Bu yordam açıklar nasıl tooconfigure Azure Mobile Engagement Android uygulamaları için çeşitli yapılandırma seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="b8579-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8579-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b8579-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="b8579-110">İzin gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="b8579-110">Permission Requirements</span></span>
<span data-ttu-id="b8579-111">Bazı seçenekler tümü burada başvuru ve satır içi hello belirli özelliği için listelenen belirli izinler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b8579-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="b8579-112">Bu izinleri toohello projenizin AndroidManifest.xml hemen önce veya sonra hello eklemek `<application>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="b8579-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="b8579-113">Merhaba izni kodu nereye hello uygun izni izleyen hello tablosundan doldurmanız hello aşağıdaki gibi toolook gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8579-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="b8579-114">İzin</span><span class="sxs-lookup"><span data-stu-id="b8579-114">Permission</span></span> | <span data-ttu-id="b8579-115">Kullanıldığında</span><span class="sxs-lookup"><span data-stu-id="b8579-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="b8579-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="b8579-116">INTERNET</span></span> |<span data-ttu-id="b8579-117">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b8579-117">Required.</span></span> <span data-ttu-id="b8579-118">Temel raporlama için</span><span class="sxs-lookup"><span data-stu-id="b8579-118">For basic reporting</span></span> |
| <span data-ttu-id="b8579-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="b8579-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="b8579-120">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b8579-120">Required.</span></span> <span data-ttu-id="b8579-121">Temel raporlama için</span><span class="sxs-lookup"><span data-stu-id="b8579-121">For basic reporting</span></span> |
| <span data-ttu-id="b8579-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="b8579-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="b8579-123">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b8579-123">Required.</span></span> <span data-ttu-id="b8579-124">tooshow hello bildirimleri merkezi aygıt yeniden başlatma işleminden sonra</span><span class="sxs-lookup"><span data-stu-id="b8579-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="b8579-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="b8579-125">WAKE_LOCK</span></span> |<span data-ttu-id="b8579-126">Önerilir.</span><span class="sxs-lookup"><span data-stu-id="b8579-126">Recommended.</span></span> <span data-ttu-id="b8579-127">WiFi kullanırken veya ekran kapalı olduğunda verilerin toplanmasını sağlar</span><span class="sxs-lookup"><span data-stu-id="b8579-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="b8579-128">TİTRET</span><span class="sxs-lookup"><span data-stu-id="b8579-128">VIBRATE</span></span> |<span data-ttu-id="b8579-129">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b8579-129">Optional.</span></span> <span data-ttu-id="b8579-130">Bildirim alındığında titreşimi sağlar</span><span class="sxs-lookup"><span data-stu-id="b8579-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="b8579-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="b8579-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="b8579-132">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b8579-132">Optional.</span></span> <span data-ttu-id="b8579-133">Android büyük resmi bildirim sağlar</span><span class="sxs-lookup"><span data-stu-id="b8579-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="b8579-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="b8579-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="b8579-135">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b8579-135">Optional.</span></span> <span data-ttu-id="b8579-136">Android büyük resmi bildirim sağlar</span><span class="sxs-lookup"><span data-stu-id="b8579-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="b8579-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="b8579-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="b8579-138">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b8579-138">Optional.</span></span> <span data-ttu-id="b8579-139">Gerçek zamanlı konum raporlama sağlar</span><span class="sxs-lookup"><span data-stu-id="b8579-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="b8579-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="b8579-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="b8579-141">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b8579-141">Optional.</span></span> <span data-ttu-id="b8579-142">GPS tabanlı konum raporlama sağlar</span><span class="sxs-lookup"><span data-stu-id="b8579-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="b8579-143">Android M ile başlayan [bazı izinler çalışma zamanında yönetilen](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="b8579-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="b8579-144">Zaten kullanıyorsanız, ``ACCESS_FINE_LOCATION``, sonra da tooalso gerekmeyen kullanmak ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="b8579-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="b8579-145">Android bildirim yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="b8579-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="b8579-146">Kilitlenme raporu</span><span class="sxs-lookup"><span data-stu-id="b8579-146">Crash report</span></span>
<span data-ttu-id="b8579-147">toodisable kilitlenme rapor, bu kod hello arasında ekleme `<application>` ve `</application>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="b8579-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="b8579-148">Eşik veri bloğu</span><span class="sxs-lookup"><span data-stu-id="b8579-148">Burst threshold</span></span>
<span data-ttu-id="b8579-149">Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b8579-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="b8579-150">Uygulama rapor günlüklerinizi sık farklılık, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları ("modu veri bloğu" olarak adlandırılır) tümünü bir defada bir normal zaman temel üzerinde.</span><span class="sxs-lookup"><span data-stu-id="b8579-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="b8579-151">toodo, bu nedenle, bu kod hello arasında ekleyin `<application>` ve `</application>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="b8579-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="b8579-152">Veri bloğu modu biraz hello pil ömrünün artırır ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olan.</span><span class="sxs-lookup"><span data-stu-id="b8579-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="b8579-153">Veri bloğu eşiği 30000 (30s) uzun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b8579-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="b8579-154">Oturum zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="b8579-154">Session timeout</span></span>
 <span data-ttu-id="b8579-155">Bir etkinlik tarafından tuşuna basarak hello sonlandırabilirsiniz **giriş** veya **geri** telefonla ayarı hello boşta veya başka bir uygulamaya atlayarak anahtar.</span><span class="sxs-lookup"><span data-stu-id="b8579-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="b8579-156">Varsayılan olarak, son etkinlik hello sonunda on saniye oturum sona erer.</span><span class="sxs-lookup"><span data-stu-id="b8579-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="b8579-157">Bu görüntüyü oluşturan hello kullanıcı Çekmeleri bağlandığınızda durum denetler bildirim, vb. her zaman hello kullanıcı çıkar ve toohello uygulama hızla döner oturum bölme önler. Bu parametre toomodify isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8579-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="b8579-158">toodo, bu nedenle, bu kod hello arasında ekleyin `<application>` ve `</application>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="b8579-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="b8579-159">Günlük bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="b8579-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="b8579-160">Yöntem çağrısı kullanma</span><span class="sxs-lookup"><span data-stu-id="b8579-160">Using a method call</span></span>
<span data-ttu-id="b8579-161">Katılım toostop günlükleri göndermek istiyorsanız, çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b8579-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="b8579-162">Bu çağrı kalıcıdır: paylaşılan tercihleri dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8579-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="b8579-163">Bu işlev çağırdığınızda katılım etkinse hello hizmet toostop bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b8579-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="b8579-164">Ancak tüm hello hello hizmeti Merhaba uygulaması sonraki başlatışınızda başlatın olmaz.</span><span class="sxs-lookup"><span data-stu-id="b8579-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="b8579-165">Aynı işlevi ile Merhaba çağırarak yeniden raporlama günlüğü etkinleştirebilirsiniz `true`.</span><span class="sxs-lookup"><span data-stu-id="b8579-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="b8579-166">Kendi tümleştirme`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="b8579-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="b8579-167">Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="b8579-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="b8579-168">Hello tercihlerinizi dosya (Merhaba istenen mod ile) katılım toouse yapılandırabilirsiniz `AndroidManifest.xml` ile dosya `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="b8579-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="b8579-169">Merhaba `engagement:agent:settings:name` kullanılan toodefine hello hello paylaşılan tercihleri dosyasının adını bir anahtardır.</span><span class="sxs-lookup"><span data-stu-id="b8579-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="b8579-170">Merhaba `engagement:agent:settings:mode` kullanılan toodefine hello modu hello paylaşılan tercihleri dosyasının bir anahtardır.</span><span class="sxs-lookup"><span data-stu-id="b8579-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="b8579-171">Kullanım hello aynı modunda olarak, `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="b8579-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="b8579-172">bir sayı olarak Hello modu geçirildi: kodunuzda sabit bayrakları birlikte kullanıyorsanız, hello toplam değerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b8579-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="b8579-173">Her zaman katılım kullanan hello `engagement:key` bu ayarı yönetmek için hello Tercihler dosyasındaki boolean anahtarı.</span><span class="sxs-lookup"><span data-stu-id="b8579-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="b8579-174">Merhaba örneği `AndroidManifest.xml` hello varsayılan değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="b8579-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="b8579-175">Ekleyebileceğiniz sonra bir `CheckBoxPreference` hello bir aşağıdaki gibi tercih düzeninde:</span><span class="sxs-lookup"><span data-stu-id="b8579-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
