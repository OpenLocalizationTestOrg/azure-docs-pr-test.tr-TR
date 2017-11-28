---
title: "Gelişmiş yapılandırma için Azure Mobile Engagement Android SDK"
description: "Android bildirim Azure Mobile Engagement Android SDK ile de dahil olmak üzere gelişmiş yapılandırma seçenekleri açıklanmaktadır"
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
ms.openlocfilehash: 0301f71c76872714aa1bf727a6c21dd7a63db036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="f0a99-103">Gelişmiş yapılandırma için Azure Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="f0a99-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0a99-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="f0a99-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="f0a99-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f0a99-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="f0a99-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f0a99-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="f0a99-107">Android</span><span class="sxs-lookup"><span data-stu-id="f0a99-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="f0a99-108">Bu yordam, Azure Mobile Engagement Android uygulamaları için çeşitli yapılandırma seçeneklerini yapılandırmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="f0a99-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0a99-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f0a99-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="f0a99-110">İzin gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="f0a99-110">Permission Requirements</span></span>
<span data-ttu-id="f0a99-111">Bazı seçenekler tümü burada başvuru ve satır içi belirli özelliği için listelenen belirli izinler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f0a99-111">Some options require specific permissions, all of which are listed here for reference, and in-line in the specific feature.</span></span> <span data-ttu-id="f0a99-112">Bu izinleri projenizin AndroidManifest.xml için hemen önce veya sonra eklemek `<application>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="f0a99-112">Add these permissions to the AndroidManifest.xml of your project immediately before or after the `<application>` tag.</span></span>

<span data-ttu-id="f0a99-113">Burada aşağıdaki tablodan uygun izni doldurmanız aşağıdaki gibi aramak izni kod gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0a99-113">The permission code needs to look like the following, where you fill in the appropriate permission from the table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="f0a99-114">İzin</span><span class="sxs-lookup"><span data-stu-id="f0a99-114">Permission</span></span> | <span data-ttu-id="f0a99-115">Kullanıldığında</span><span class="sxs-lookup"><span data-stu-id="f0a99-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="f0a99-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="f0a99-116">INTERNET</span></span> |<span data-ttu-id="f0a99-117">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="f0a99-117">Required.</span></span> <span data-ttu-id="f0a99-118">Temel raporlama için</span><span class="sxs-lookup"><span data-stu-id="f0a99-118">For basic reporting</span></span> |
| <span data-ttu-id="f0a99-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="f0a99-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="f0a99-120">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="f0a99-120">Required.</span></span> <span data-ttu-id="f0a99-121">Temel raporlama için</span><span class="sxs-lookup"><span data-stu-id="f0a99-121">For basic reporting</span></span> |
| <span data-ttu-id="f0a99-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="f0a99-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="f0a99-123">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="f0a99-123">Required.</span></span> <span data-ttu-id="f0a99-124">Cihaz yeniden başlatıldıktan sonra bildirimleri center göstermek için</span><span class="sxs-lookup"><span data-stu-id="f0a99-124">To show up the notifications center after device reboot</span></span> |
| <span data-ttu-id="f0a99-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="f0a99-125">WAKE_LOCK</span></span> |<span data-ttu-id="f0a99-126">Önerilir.</span><span class="sxs-lookup"><span data-stu-id="f0a99-126">Recommended.</span></span> <span data-ttu-id="f0a99-127">WiFi kullanırken veya ekran kapalı olduğunda verilerin toplanmasını sağlar</span><span class="sxs-lookup"><span data-stu-id="f0a99-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="f0a99-128">TİTRET</span><span class="sxs-lookup"><span data-stu-id="f0a99-128">VIBRATE</span></span> |<span data-ttu-id="f0a99-129">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f0a99-129">Optional.</span></span> <span data-ttu-id="f0a99-130">Bildirim alındığında titreşimi sağlar</span><span class="sxs-lookup"><span data-stu-id="f0a99-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="f0a99-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="f0a99-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="f0a99-132">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f0a99-132">Optional.</span></span> <span data-ttu-id="f0a99-133">Android büyük resmi bildirim sağlar</span><span class="sxs-lookup"><span data-stu-id="f0a99-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="f0a99-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="f0a99-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="f0a99-135">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f0a99-135">Optional.</span></span> <span data-ttu-id="f0a99-136">Android büyük resmi bildirim sağlar</span><span class="sxs-lookup"><span data-stu-id="f0a99-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="f0a99-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="f0a99-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="f0a99-138">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f0a99-138">Optional.</span></span> <span data-ttu-id="f0a99-139">Gerçek zamanlı konum raporlama sağlar</span><span class="sxs-lookup"><span data-stu-id="f0a99-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="f0a99-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="f0a99-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="f0a99-141">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f0a99-141">Optional.</span></span> <span data-ttu-id="f0a99-142">GPS tabanlı konum raporlama sağlar</span><span class="sxs-lookup"><span data-stu-id="f0a99-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="f0a99-143">Android M ile başlayan [bazı izinler çalışma zamanında yönetilen](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="f0a99-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="f0a99-144">Zaten kullanıyorsanız, ``ACCESS_FINE_LOCATION``, ayrıca kullanmanız gerekmez sonra ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="f0a99-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need to also use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="f0a99-145">Android bildirim yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f0a99-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="f0a99-146">Kilitlenme raporu</span><span class="sxs-lookup"><span data-stu-id="f0a99-146">Crash report</span></span>
<span data-ttu-id="f0a99-147">Kilitlenme raporları devre dışı bırakmak için bu kodu arasında ekleyin `<application>` ve `</application>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="f0a99-147">To disable crash reports, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="f0a99-148">Eşik veri bloğu</span><span class="sxs-lookup"><span data-stu-id="f0a99-148">Burst threshold</span></span>
<span data-ttu-id="f0a99-149">Varsayılan olarak, katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f0a99-149">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="f0a99-150">Uygulama rapor günlüklerinizi sık farklılık, günlükleri arabellek ve üzerlerinde tümünü bir defada bir normal zaman temel ("modu veri bloğu" olarak adlandırılır) bildirmek için daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="f0a99-150">If your application report logs vary frequently, it is better to buffer the logs and to report them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="f0a99-151">Bunu yapmak için bu kod arasında eklemek `<application>` ve `</application>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="f0a99-151">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="f0a99-152">Veri bloğu modu biraz pil ömrünün artırır ancak Engagement İzleyicisi üzerinde bir etkisi vardır: tüm oturumları ve işleri süre (dolayısıyla, oturumlar ve işleri veri bloğu eşik görünmeyebilir daha kısa) veri bloğu eşik yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0a99-152">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="f0a99-153">Veri bloğu eşiği 30000 (30s) uzun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0a99-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="f0a99-154">Oturum zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="f0a99-154">Session timeout</span></span>
 <span data-ttu-id="f0a99-155">Tuşuna basarak bir etkinlik sonlandırabilirsiniz **giriş** veya **geri** ayarlayarak telefon boşta veya başka bir uygulamaya atlayarak anahtar.</span><span class="sxs-lookup"><span data-stu-id="f0a99-155">You can end an activity by pressing the **Home** or **Back** key, by setting the phone idle or by jumping into another application.</span></span> <span data-ttu-id="f0a99-156">Varsayılan olarak, son etkinlik sonunda on saniye oturumu sona erer.</span><span class="sxs-lookup"><span data-stu-id="f0a99-156">By default, a session is ended ten seconds after the end of its last activity.</span></span> <span data-ttu-id="f0a99-157">Bu, görüntüyü oluşturan kullanıcının Çekmeleri bağlandığınızda durum denetler bildirim, vb. kullanıcı çıkar ve hızlı bir şekilde, uygulamaya döndürür her zaman bir oturum bölme önler. Bu parametre değiştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0a99-157">This avoids a session split each time the user exits and returns to the application quickly, which can happen when the user picks up an image, checks a notification, etc. You may want to modify this parameter.</span></span> <span data-ttu-id="f0a99-158">Bunu yapmak için bu kod arasında eklemek `<application>` ve `</application>` etiketler:</span><span class="sxs-lookup"><span data-stu-id="f0a99-158">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="f0a99-159">Günlük bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f0a99-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="f0a99-160">Yöntem çağrısı kullanma</span><span class="sxs-lookup"><span data-stu-id="f0a99-160">Using a method call</span></span>
<span data-ttu-id="f0a99-161">Engagement'ın günlükleri göndermek durdurmak istiyorsanız, çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f0a99-161">If you want Engagement to stop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="f0a99-162">Bu çağrı kalıcıdır: paylaşılan tercihleri dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="f0a99-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="f0a99-163">Bu işlev çağırdığınızda katılım etkinse durdurmak hizmet için bir dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f0a99-163">If Engagement is active when you call this function, it may take one minute for the service to stop.</span></span> <span data-ttu-id="f0a99-164">Hizmeti her başlatıldığında başlatın olmaz ancak uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="f0a99-164">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="f0a99-165">Yeniden ile aynı işlevini çağırarak raporlama günlüğü etkinleştirebilirsiniz `true`.</span><span class="sxs-lookup"><span data-stu-id="f0a99-165">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="f0a99-166">Kendi tümleştirme`PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="f0a99-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="f0a99-167">Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f0a99-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="f0a99-168">Tercihler dosyanız (istenen moduyla) kullanmak için katılım yapılandırabileceğiniz `AndroidManifest.xml` ile dosya `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="f0a99-168">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="f0a99-169">`engagement:agent:settings:name` Anahtar paylaşılan tercihleri dosya adını tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0a99-169">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="f0a99-170">`engagement:agent:settings:mode` Anahtar paylaşılan tercihleri dosya modunu tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0a99-170">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file.</span></span> <span data-ttu-id="f0a99-171">Aynı modunda olarak kullanmak, `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f0a99-171">Use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="f0a99-172">Mod bir sayı olarak geçirilmelidir: kodunuzda sabit bayrakları birlikte kullanıyorsanız, toplam değerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f0a99-172">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="f0a99-173">Her zaman katılım kullanan `engagement:key` boolean anahtarı bu ayarı yönetmek için Tercihler dosya içinde.</span><span class="sxs-lookup"><span data-stu-id="f0a99-173">Engagement always uses the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="f0a99-174">Aşağıdaki örnekte `AndroidManifest.xml` varsayılan değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="f0a99-174">The following example of `AndroidManifest.xml` shows the default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="f0a99-175">Ekleyebileceğiniz sonra bir `CheckBoxPreference` , tercih yerleşiminde aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="f0a99-175">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
