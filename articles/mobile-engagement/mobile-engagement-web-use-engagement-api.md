---
title: Azure Mobile Engagement Web SDK API'leri | Microsoft Docs
description: "En son güncelleştirmeleri ve Azure Mobile Engagement için Web SDK'sı için yordamlar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="7534c-103">Bir web uygulamasına Azure Mobile Engagement API kullanın</span><span class="sxs-lookup"><span data-stu-id="7534c-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="7534c-104">Bu belge nasıl söyler belgeye bir ektir için [Mobile Engagement bir web uygulaması tümleştirme](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="7534c-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="7534c-105">Azure Mobile Engagement API uygulama istatistikleri rapor için nasıl kullanılacağı hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7534c-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="7534c-106">Mobile Engagement API'si tarafından sağlanan `engagement.agent` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7534c-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="7534c-107">Azure Mobile Engagement Web SDK diğer adı olan varsayılan `engagement`.</span><span class="sxs-lookup"><span data-stu-id="7534c-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="7534c-108">Bu diğer adı SDK yapılandırmasından tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7534c-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="7534c-109">Mobile Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="7534c-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="7534c-110">Aşağıdaki bölümleri ortak İyileştir [Mobile Engagement kavramları](mobile-engagement-concepts.md) web platformu için.</span><span class="sxs-lookup"><span data-stu-id="7534c-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="7534c-111">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="7534c-111">`Session` and `Activity`</span></span>
<span data-ttu-id="7534c-112">Kullanıcı iki etkinlik arasında birden fazla birkaç saniye boyunca boşta kalırsa, kullanıcının etkinlikler dizisini iki ayrı oturumlara ayrılır.</span><span class="sxs-lookup"><span data-stu-id="7534c-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="7534c-113">Bu birkaç saniye oturum zaman aşımı denir.</span><span class="sxs-lookup"><span data-stu-id="7534c-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="7534c-114">Web uygulamanız kullanıcı etkinlikleri sonuna tek başına bildirme değil ise (çağırarak `engagement.agent.endActivity` işlevi), Mobile Engagement sunucunun otomatik olarak kullanıcı oturumunun üç uygulama sayfası kapatıldıktan sonra dakika içinde süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="7534c-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="7534c-115">Bu sunucu oturum zaman aşımı çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7534c-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="7534c-116">Yakalanmayan JavaScript özel durumlarının otomatik raporları varsayılan olarak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="7534c-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="7534c-117">Kilitlenme ancak rapor kullanarak el ile `sendCrash` (kilitlenme bildirimi bölümüne bakın) işlev.</span><span class="sxs-lookup"><span data-stu-id="7534c-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="7534c-118">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="7534c-118">Reporting activities</span></span>
<span data-ttu-id="7534c-119">Kullanıcı etkinliğini raporlama, bir kullanıcı yeni bir etkinlik başlatıldığında ve kullanıcı geçerli etkinliği sona erdiğinde içerir.</span><span class="sxs-lookup"><span data-stu-id="7534c-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="7534c-120">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="7534c-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="7534c-121">Çağırmanız gerekir `startActivity()` her zaman kullanıcı etkinliği değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7534c-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="7534c-122">Bu işlev ilk çağrıda yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="7534c-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="7534c-123">Kullanıcı geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="7534c-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="7534c-124">Çağırmanız gerekir `endActivity()` en az bir kez kullanıcı tamamlandığında son etkinliklerini.</span><span class="sxs-lookup"><span data-stu-id="7534c-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="7534c-125">Bu Mobile Engagement Web SDK'sı kullanıcının şu anda boş olduğunu ve kullanıcı oturumunu oturum zaman aşımı süresi dolduktan sonra kapalı olması gerektiğini bildirir.</span><span class="sxs-lookup"><span data-stu-id="7534c-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="7534c-126">Çağırırsanız `startActivity()` oturum, yalnızca oturum zaman aşımı süresi dolmadan önce devam ettirilir.</span><span class="sxs-lookup"><span data-stu-id="7534c-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="7534c-127">Güvenilir arama Gezgini penceresi kapatıldığında yok olduğundan, genellikle zor veya bir web ortamı içindeki kullanıcı etkinlikleri sonuna catch mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="7534c-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="7534c-128">İşte bu nedenle Mobile Engagement sunucunun otomatik olarak kullanıcı oturumunun üç uygulama sayfası kapatıldıktan sonra dakika içinde süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="7534c-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="7534c-129">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="7534c-129">Reporting events</span></span>
<span data-ttu-id="7534c-130">Raporlama olayları üzerinde oturum olayları ve tek başına olayları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7534c-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="7534c-131">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="7534c-131">Session events</span></span>
<span data-ttu-id="7534c-132">Oturum olaylar, genellikle kullanıcının oturumu sırasında bir kullanıcı tarafından gerçekleştirilen eylemleri bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7534c-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="7534c-133">**Ek veriler olmadan örneği:**</span><span class="sxs-lookup"><span data-stu-id="7534c-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="7534c-134">**Örnek ek veriler ile:**</span><span class="sxs-lookup"><span data-stu-id="7534c-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="7534c-135">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="7534c-135">Standalone events</span></span>
<span data-ttu-id="7534c-136">Oturum olayları, bir oturum bağlamı dışında tek başına olaylar gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="7534c-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="7534c-137">Bunun için kullanmak ``engagement.agent.sendEvent`` yerine ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="7534c-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="7534c-138">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="7534c-138">Reporting errors</span></span>
<span data-ttu-id="7534c-139">Hata raporlama, oturum hataları ve tek başına hataları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7534c-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="7534c-140">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="7534c-140">Session errors</span></span>
<span data-ttu-id="7534c-141">Oturum hatalar genellikle bir etkisi kullanıcının oturumu sırasında kullanıcıya hatalarını bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7534c-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="7534c-142">**Ek veriler olmadan örneği:**</span><span class="sxs-lookup"><span data-stu-id="7534c-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="7534c-143">**Örnek ek veriler ile:**</span><span class="sxs-lookup"><span data-stu-id="7534c-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="7534c-144">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="7534c-144">Standalone errors</span></span>
<span data-ttu-id="7534c-145">Oturum hatalarının aksine, bir oturum bağlamı dışında tek başına hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="7534c-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="7534c-146">Bunun için kullanmak `engagement.agent.sendError` yerine `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="7534c-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="7534c-147">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="7534c-147">Reporting jobs</span></span>
<span data-ttu-id="7534c-148">Raporlama, hataları ve bir işi sırasında meydana gelen olayları raporlama ve kilitlenme raporlama işleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="7534c-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="7534c-149">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="7534c-149">**Example:**</span></span>

<span data-ttu-id="7534c-150">AJAX isteği izlemek istiyorsanız, aşağıdaki kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="7534c-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="7534c-151">Bir işi sırasında hata raporlama</span><span class="sxs-lookup"><span data-stu-id="7534c-151">Reporting errors during a job</span></span>
<span data-ttu-id="7534c-152">Hataları geçerli kullanıcı oturum çalışan bir işi yerine ile ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="7534c-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="7534c-153">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="7534c-153">**Example:**</span></span>

<span data-ttu-id="7534c-154">Bir AJAX isteği başarısız olursa bir hata raporu istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="7534c-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="7534c-155">Raporlama işi sırasında olayları</span><span class="sxs-lookup"><span data-stu-id="7534c-155">Reporting events during a job</span></span>
<span data-ttu-id="7534c-156">Olaylar ilgili olabileceğini yerine çalıştırılan bir iş geçerli kullanıcı oturum teşekkürler `engagement.agent.sendJobEvent` işlevi.</span><span class="sxs-lookup"><span data-stu-id="7534c-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="7534c-157">Bu işlev tıpkı `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="7534c-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="7534c-158">Kilitlenme raporlama</span><span class="sxs-lookup"><span data-stu-id="7534c-158">Reporting crashes</span></span>
<span data-ttu-id="7534c-159">Kullanım `sendCrash` rapor işleve çöküyor el ile.</span><span class="sxs-lookup"><span data-stu-id="7534c-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="7534c-160">`crashid` Kilitlenme türünü tanımlayan bir dize bağımsız değişkeni aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="7534c-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="7534c-161">`crash` Genellikle olmayan bağımsız değişken bir dize olarak kilitlenme yığın izlemesi.</span><span class="sxs-lookup"><span data-stu-id="7534c-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="7534c-162">Ek parametreler</span><span class="sxs-lookup"><span data-stu-id="7534c-162">Extra parameters</span></span>
<span data-ttu-id="7534c-163">Bir olay, hata, etkinlik veya iş için rasgele verileri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7534c-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="7534c-164">Veriler, herhangi bir JSON nesnesi (ancak bir dizi veya ilkel tür) olabilir.</span><span class="sxs-lookup"><span data-stu-id="7534c-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="7534c-165">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="7534c-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="7534c-166">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="7534c-166">Limits</span></span>
<span data-ttu-id="7534c-167">Ek parametreler geçerli anahtarları, değer türleri ve boyutu için normal ifadeler alanlarda kısıtlamalardır.</span><span class="sxs-lookup"><span data-stu-id="7534c-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="7534c-168">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="7534c-168">Keys</span></span>
<span data-ttu-id="7534c-169">Nesne tablosundaki her anahtarın şu normal ifadeyle aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7534c-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="7534c-170">Anahtarları en az bir harf ile başlamalıdır Bunun anlamı arkasından harf, rakam veya alt çizgi ile (\_).</span><span class="sxs-lookup"><span data-stu-id="7534c-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="7534c-171">Değerler</span><span class="sxs-lookup"><span data-stu-id="7534c-171">Values</span></span>
<span data-ttu-id="7534c-172">Dize, sayı ve Boolean türleri için sınırlı değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="7534c-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="7534c-173">Boyut</span><span class="sxs-lookup"><span data-stu-id="7534c-173">Size</span></span>
<span data-ttu-id="7534c-174">(Mobile Engagement Web SDK'sı, JSON'da kodlar) sonra ek özellikler çağrı başına 1024 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="7534c-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="7534c-175">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="7534c-175">Reporting application information</span></span>
<span data-ttu-id="7534c-176">El ile (veya başka bir uygulamaya özgü bilgileri) izleme kullanarak raporlayabilirsiniz `sendAppInfo()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="7534c-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="7534c-177">Bu bilgi artımlı olarak gönderilebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7534c-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="7534c-178">Belirli bir aygıt için belirli bir anahtarın yalnızca en son değeri korunur.</span><span class="sxs-lookup"><span data-stu-id="7534c-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="7534c-179">Olay ek özellikler gibi uygulama bilgilerini soyut için herhangi bir JSON nesnesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7534c-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="7534c-180">Diziler veya alt nesneler (JSON serileştirmesi kullanan) düz dize olarak davranılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7534c-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="7534c-181">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="7534c-181">**Example:**</span></span>

<span data-ttu-id="7534c-182">Kullanıcının cinsiyeti ve doğum tarihi göndermek için bir kod örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7534c-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="7534c-183">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="7534c-183">Limits</span></span>
<span data-ttu-id="7534c-184">Uygulama bilgilerini uygulanan anahtarları ve boyutu için normal ifadeler alanlarda kısıtlamalardır.</span><span class="sxs-lookup"><span data-stu-id="7534c-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="7534c-185">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="7534c-185">Keys</span></span>
<span data-ttu-id="7534c-186">Nesne tablosundaki her anahtarın şu normal ifadeyle aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7534c-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="7534c-187">Anahtarları en az bir harf ile başlamalıdır Bunun anlamı arkasından harf, rakam veya alt çizgi ile (\_).</span><span class="sxs-lookup"><span data-stu-id="7534c-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="7534c-188">Boyut</span><span class="sxs-lookup"><span data-stu-id="7534c-188">Size</span></span>
<span data-ttu-id="7534c-189">(Mobile Engagement Web SDK'sı, JSON'da kodlar sonra) uygulama bilgilerini çağrı başına 1024 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="7534c-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="7534c-190">Önceki örnekte, sunucuya gönderilen JSON 44 karakter olacak:</span><span class="sxs-lookup"><span data-stu-id="7534c-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
