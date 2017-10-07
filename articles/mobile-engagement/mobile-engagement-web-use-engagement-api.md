---
title: Mobile Engagement Web SDK API'leri aaaAzure | Microsoft Docs
description: "en son güncelleştirmeler ve yordamlar hello Web SDK'sı için Azure Mobile Engagement için hello"
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="4d6e8-103">Bir web uygulaması Hello Azure Mobile Engagement API kullanın</span><span class="sxs-lookup"><span data-stu-id="4d6e8-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="4d6e8-104">Bu belge nasıl çok belirten bir toplama toohello belgesidir[Mobile Engagement bir web uygulaması tümleştirme](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="4d6e8-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="4d6e8-105">Bu, uygulama istatistikleri nasıl toouse hello Azure Mobile Engagement API tooreport hakkında kapsamlı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="4d6e8-106">Merhaba Mobile Engagement API hello tarafından sağlanan `engagement.agent` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="4d6e8-107">Merhaba varsayılan Azure Mobile Engagement Web SDK diğer `engagement`.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="4d6e8-108">Bu diğer adı hello SDK yapılandırmasından tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="4d6e8-109">Mobile Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="4d6e8-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="4d6e8-110">Merhaba aşağıdaki bölümleri ortak İyileştir [Mobile Engagement kavramları](mobile-engagement-concepts.md) hello web platformu için.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="4d6e8-111">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="4d6e8-111">`Session` and `Activity`</span></span>
<span data-ttu-id="4d6e8-112">Merhaba kullanıcı iki etkinlik arasında birden fazla birkaç saniye boyunca boşta kalırsa, hello kullanıcının etkinlikler dizisini iki ayrı oturumlara ayrılır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="4d6e8-113">Bu birkaç saniye hello oturum zaman aşımı denir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="4d6e8-114">Web uygulamanız kullanıcı etkinlikleri hello sonuna tek başına bildirme değil ise (arama hello tarafından `engagement.agent.endActivity` işlevi), hello Mobile Engagement sunucu otomatik olarak sona hello üç hello uygulama sayfası kapatıldıktan sonra dakika içinde kullanıcı oturumu.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="4d6e8-115">Bu hello sunucu oturum zaman aşımı çağrılır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="4d6e8-116">Yakalanmayan JavaScript özel durumlarının otomatik raporları varsayılan olarak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="4d6e8-117">Kilitlenme ancak rapor hello kullanarak el ile `sendCrash` (kilitlenme bildirimi hello bölümüne bakın) işlev.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="4d6e8-118">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="4d6e8-118">Reporting activities</span></span>
<span data-ttu-id="4d6e8-119">Kullanıcı etkinliğini raporlama, bir kullanıcı yeni bir etkinlik başladığında ve hello kullanıcı hello geçerli etkinliği sona erdiğinde içerir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="4d6e8-120">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="4d6e8-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="4d6e8-121">Toocall gerek `startActivity()` her zaman kullanıcı etkinliği değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="4d6e8-122">Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="4d6e8-123">Kullanıcı hello geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="4d6e8-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="4d6e8-124">Toocall gerek `endActivity()` en az bir kez hello kullanıcı tamamlandığında son etkinliklerini.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="4d6e8-125">Bu hello Mobile Engagement Web SDK hello kullanıcı şu anda boşta kalır ve hello kullanıcı oturumu toobe gerektiğini hello oturum zaman aşımı süresi dolduktan sonra kapalı bildirir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="4d6e8-126">Çağırırsanız `startActivity()` hello oturum, yalnızca hello oturum zaman aşımı süresi dolmadan önce devam ettirilir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="4d6e8-127">Merhaba Gezgini penceresi kapatıldığında için güvenilir bir çağrı yok olduğundan genellikle web ortamı içindeki kullanıcı etkinlikleri zor veya olanaksız toocatch hello sonuna değildir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="4d6e8-128">Olduğu neden hello Mobile Engagement sunucu otomatik olarak sona hello kullanıcı oturumunu üç hello uygulama sayfası kapatıldıktan sonra dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="4d6e8-129">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="4d6e8-129">Reporting events</span></span>
<span data-ttu-id="4d6e8-130">Raporlama olayları üzerinde oturum olayları ve tek başına olayları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="4d6e8-131">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="4d6e8-131">Session events</span></span>
<span data-ttu-id="4d6e8-132">Oturum genellikle kullanılan tooreport hello Eylemler hello kullanıcının oturumu sırasında bir kullanıcı tarafından gerçekleştirilen olaylardır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="4d6e8-133">**Ek veriler olmadan örneği:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="4d6e8-134">**Örnek ek veriler ile:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="4d6e8-135">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="4d6e8-135">Standalone events</span></span>
<span data-ttu-id="4d6e8-136">Oturum olayları, bir oturum hello bağlamı dışında tek başına olaylar gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="4d6e8-137">Bunun için kullanmak ``engagement.agent.sendEvent`` yerine ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="4d6e8-138">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="4d6e8-138">Reporting errors</span></span>
<span data-ttu-id="4d6e8-139">Hata raporlama, oturum hataları ve tek başına hataları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="4d6e8-140">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="4d6e8-140">Session errors</span></span>
<span data-ttu-id="4d6e8-141">Oturum hatalar genellikle bir etkisi hello kullanıcının oturumu sırasında hello kullanıcı kullanılan tooreport hello hatalardır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="4d6e8-142">**Ek veriler olmadan örneği:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="4d6e8-143">**Örnek ek veriler ile:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="4d6e8-144">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="4d6e8-144">Standalone errors</span></span>
<span data-ttu-id="4d6e8-145">Oturum hatalarının aksine, bir oturum hello bağlamı dışında tek başına hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="4d6e8-146">Bunun için kullanmak `engagement.agent.sendError` yerine `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="4d6e8-147">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="4d6e8-147">Reporting jobs</span></span>
<span data-ttu-id="4d6e8-148">Raporlama, hataları ve bir işi sırasında meydana gelen olayları raporlama ve kilitlenme raporlama işleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="4d6e8-149">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-149">**Example:**</span></span>

<span data-ttu-id="4d6e8-150">Toomonitor bir AJAX isteği istiyorsanız hello aşağıdaki kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="4d6e8-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="4d6e8-151">Bir işi sırasında hata raporlama</span><span class="sxs-lookup"><span data-stu-id="4d6e8-151">Reporting errors during a job</span></span>
<span data-ttu-id="4d6e8-152">Hataları toohello geçerli kullanıcı oturumunun yerine işi ilgili tooa olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="4d6e8-153">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-153">**Example:**</span></span>

<span data-ttu-id="4d6e8-154">Tooreport bir AJAX isteği varsa bir hata istiyorsanız başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="4d6e8-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="4d6e8-155">Raporlama işi sırasında olayları</span><span class="sxs-lookup"><span data-stu-id="4d6e8-155">Reporting events during a job</span></span>
<span data-ttu-id="4d6e8-156">Olaylar, ilgili tooa toohello geçerli kullanıcı oturumunun yerine thanks toohello işi olabilir `engagement.agent.sendJobEvent` işlevi.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="4d6e8-157">Bu işlev tıpkı `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="4d6e8-158">Kilitlenme raporlama</span><span class="sxs-lookup"><span data-stu-id="4d6e8-158">Reporting crashes</span></span>
<span data-ttu-id="4d6e8-159">Kullanım hello `sendCrash` işlevi tooreport çöküyor el ile.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="4d6e8-160">Merhaba `crashid` değişkendir hello kilitlenme türünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="4d6e8-161">Merhaba `crash` genellikle olmayan bağımsız değişken bir dize olarak hello kilitlenme hello yığın izlemesi.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="4d6e8-162">Ek parametreler</span><span class="sxs-lookup"><span data-stu-id="4d6e8-162">Extra parameters</span></span>
<span data-ttu-id="4d6e8-163">Rastgele veri tooan olayı, hata, etkinlik veya iş ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="4d6e8-164">Merhaba veriler herhangi bir JSON nesnesi (ancak bir dizi veya ilkel tür) olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="4d6e8-165">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="4d6e8-166">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="4d6e8-166">Limits</span></span>
<span data-ttu-id="4d6e8-167">Tooextra parametreleri geçerli anahtarları, değer türleri ve boyutu için normal ifadeler hello alanlarında kısıtlamalardır.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="4d6e8-168">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="4d6e8-168">Keys</span></span>
<span data-ttu-id="4d6e8-169">Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d6e8-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="4d6e8-170">Anahtarları en az bir harf ile başlamalıdır Bunun anlamı arkasından harf, rakam veya alt çizgi ile (\_).</span><span class="sxs-lookup"><span data-stu-id="4d6e8-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="4d6e8-171">Değerler</span><span class="sxs-lookup"><span data-stu-id="4d6e8-171">Values</span></span>
<span data-ttu-id="4d6e8-172">Sınırlı toostring, sayı ve Boolean türleri değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="4d6e8-173">Boyut</span><span class="sxs-lookup"><span data-stu-id="4d6e8-173">Size</span></span>
<span data-ttu-id="4d6e8-174">Ek özellikler sınırlı too1, (Merhaba Mobile Engagement Web SDK'sı, JSON'da kodlar sonra) çağrı başına 024 karakterler var.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="4d6e8-175">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="4d6e8-175">Reporting application information</span></span>
<span data-ttu-id="4d6e8-176">El ile (veya başka bir uygulamaya özgü bilgileri) izleme hello kullanarak raporlayabilirsiniz `sendAppInfo()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="4d6e8-177">Bu bilgi artımlı olarak gönderilebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="4d6e8-178">Belirli bir aygıt için yalnızca en son değerini belirli bir anahtarın hello tutulacak.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="4d6e8-179">Olay ek özellikler gibi herhangi bir JSON nesnesi tooabstract uygulama bilgi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="4d6e8-180">Diziler veya alt nesneler (JSON serileştirmesi kullanan) düz dize olarak davranılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="4d6e8-181">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="4d6e8-181">**Example:**</span></span>

<span data-ttu-id="4d6e8-182">Gönderen hello kullanıcının cinsiyeti ve doğum tarihi bir kod örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4d6e8-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="4d6e8-183">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="4d6e8-183">Limits</span></span>
<span data-ttu-id="4d6e8-184">Anahtarları ve boyutu için normal ifadeler hello alanlarında tooapplication bilgiler geçerli sınırı mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="4d6e8-185">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="4d6e8-185">Keys</span></span>
<span data-ttu-id="4d6e8-186">Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d6e8-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="4d6e8-187">Anahtarları en az bir harf ile başlamalıdır Bunun anlamı arkasından harf, rakam veya alt çizgi ile (\_).</span><span class="sxs-lookup"><span data-stu-id="4d6e8-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="4d6e8-188">Boyut</span><span class="sxs-lookup"><span data-stu-id="4d6e8-188">Size</span></span>
<span data-ttu-id="4d6e8-189">Uygulama, sınırlı too1, 024 karakterleri (Merhaba Mobile Engagement Web SDK'sı, JSON'da kodlar sonra) çağrı başına bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="4d6e8-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="4d6e8-190">Örnek önceki hello hello JSON toohello sunucu 44 karakter uzunluğunda gönderilir:</span><span class="sxs-lookup"><span data-stu-id="4d6e8-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
