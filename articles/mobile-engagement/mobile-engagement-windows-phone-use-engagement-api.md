---
title: "aaaHow tooUse hello Windows Phone Silverlight katılım API"
description: "Nasıl tooUse hello Windows Phone Silverlight katılım API"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="59607-103">Nasıl tooUse hello Windows Phone Silverlight katılım API</span><span class="sxs-lookup"><span data-stu-id="59607-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="59607-104">Bu belge bir eklenti toohello belgesidir [nasıl toointegrate Mobile Engagement Windows Phone Silverlight uygulamanızda](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="59607-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="59607-105">Nasıl toouse hello katılım API tooreport uygulama istatistikleri hakkında ayrıntılar derinliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="59607-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="59607-106">Yalnızca katılım tooreport uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgi istiyorsanız sonra hello en basit yolu toomake tüm olduğundan, `PhoneApplicationPage` alt sınıfları devral hello `EngagementPage` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="59607-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="59607-107">Daha fazla tooreport uygulama belirli olaylar, hatalar ve işleri gerekiyorsa örneğin toodo istiyorsanız veya tooreport uygulamanızın etkinlikleri farklı bir şekilde bir hello uygulanan hello daha varsa `EngagementPage` sınıfları yeniden toouse hello gerekiyor Katılım API.</span><span class="sxs-lookup"><span data-stu-id="59607-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="59607-108">Merhaba katılım API hello tarafından sağlanan `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="59607-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="59607-109">Toothose yöntemlerle erişebilirsiniz `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="59607-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="59607-110">Merhaba aracı modülü başlatılmadı olsa bile, her çağrı toohello API ertelenir ve hello Aracısı kullanılabilir olduğunda yeniden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="59607-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="59607-111">Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="59607-111">Engagement concepts</span></span>
<span data-ttu-id="59607-112">bölümleri aşağıdaki hello hello Mobile Engagement kavramları hello Windows Phone platform için yenileyin.</span><span class="sxs-lookup"><span data-stu-id="59607-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="59607-113">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="59607-113">`Session` and `Activity`</span></span>
<span data-ttu-id="59607-114">Bir *etkinlik* genellikle toosay hello hello uygulama, bir sayfayla ilişkili *etkinlik* hello sayfası görüntülenir ve hello sayfa kapatıldığında durdurduğunda başlatır: hello hello zaman böyledir Engagement SDK'sı tümleşik hello kullanarak `EngagementPage` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="59607-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="59607-115">Ancak *etkinlikleri* de el ile Merhaba katılım API kullanılarak denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="59607-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="59607-116">Bu toosplit belirli bir sayfa hakkında daha fazla ayrıntı (örneğin tooknown ne sıklıkta ve ne kadar süre içinde bu sayfa iletişim kutuları kullanılır), bu sayfanın kullanım hello birkaç alt bölümleri tooget sağlar.</span><span class="sxs-lookup"><span data-stu-id="59607-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="59607-117">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="59607-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="59607-118">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="59607-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-119">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-120">Toocall gerek `StartActivity()` her zaman hello kullanıcı etkinliği değiştirir.</span><span class="sxs-lookup"><span data-stu-id="59607-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="59607-121">Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="59607-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59607-122">Merhaba SDK otomatik olarak çağrı hello EndActivity yöntemi hello uygulama kapatıldığında.</span><span class="sxs-lookup"><span data-stu-id="59607-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="59607-123">Bu nedenle, hello kullanıcı değiştirme ve hello EndActivity yöntemi, bu yöntemi çağırmadan itibaren hello geçerli oturum toobe zorlar tooNEVER çağrı Hello etkinliğini sona erdi her toocall hello StartActivity yöntemi KULLANMAMANIZ önerilir.</span><span class="sxs-lookup"><span data-stu-id="59607-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="59607-124">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="59607-125">Kullanıcı kendi geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="59607-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-126">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="59607-127">Toocall gerek `EndActivity()` en az bir kez hello kullanıcı tamamlandığında son etkinliğini.</span><span class="sxs-lookup"><span data-stu-id="59607-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="59607-128">Bu Engagement SDK'sı hello kullanıcı şu anda boşta ve hello kullanıcı oturumu toobe gerektiğini bildiren bir kez hello oturum zaman aşımı kapalı dolacak hello bildirir (çağırırsanız `StartActivity()` hello oturum, yalnızca hello oturum zaman aşımı süresi dolmadan önce devam ettirildiğinde).</span><span class="sxs-lookup"><span data-stu-id="59607-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="59607-129">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="59607-130">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="59607-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="59607-131">Bir işi Başlat</span><span class="sxs-lookup"><span data-stu-id="59607-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-132">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-133">Bir süre boyunca hello iş tootrack bazı görevleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59607-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="59607-135">Bir işin bitiş</span><span class="sxs-lookup"><span data-stu-id="59607-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-136">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="59607-137">Bir iş tarafından izlenen bir görev sonlandırıldı hemen hello iş adı sağlayarak bu proje için hello EndJob yöntemini çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="59607-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-138">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="59607-139">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="59607-139">Reporting Events</span></span>
<span data-ttu-id="59607-140">Üç tür olay vardır:</span><span class="sxs-lookup"><span data-stu-id="59607-140">There is three types of events :</span></span>

* <span data-ttu-id="59607-141">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="59607-141">Standalone events</span></span>
* <span data-ttu-id="59607-142">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="59607-142">Session events</span></span>
* <span data-ttu-id="59607-143">İş olayları</span><span class="sxs-lookup"><span data-stu-id="59607-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="59607-144">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="59607-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-145">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-146">Tek başına olaylar oturumu hello bağlamı dışında gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="59607-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-147">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="59607-148">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="59607-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-149">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-150">Oturum, kendi oturumunda bir kullanıcı tarafından gerçekleştirilen genellikle kullanılan tooreport hello Eylemler olaylardır.</span><span class="sxs-lookup"><span data-stu-id="59607-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-151">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-151">Example</span></span>
<span data-ttu-id="59607-152">**Veri olmadan:**</span><span class="sxs-lookup"><span data-stu-id="59607-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="59607-153">**Verilerle:**</span><span class="sxs-lookup"><span data-stu-id="59607-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="59607-154">İş olayları</span><span class="sxs-lookup"><span data-stu-id="59607-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-155">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-156">İş, bir kullanıcı tarafından gerçekleştirilen işi sırasında genellikle kullanılan tooreport hello Eylemler olaylardır.</span><span class="sxs-lookup"><span data-stu-id="59607-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-157">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="59607-158">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="59607-158">Reporting Errors</span></span>
<span data-ttu-id="59607-159">Üç tür hataları vardır:</span><span class="sxs-lookup"><span data-stu-id="59607-159">There is three types of errors :</span></span>

* <span data-ttu-id="59607-160">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="59607-160">Standalone errors</span></span>
* <span data-ttu-id="59607-161">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="59607-161">Session errors</span></span>
* <span data-ttu-id="59607-162">İş hataları</span><span class="sxs-lookup"><span data-stu-id="59607-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="59607-163">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="59607-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-164">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-165">Bulmadýðýný toosession hataları, bir oturum Merhaba içeriğine dışında tek başına hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="59607-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-166">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="59607-167">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="59607-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-168">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-169">Oturum hatalar hello kullanıcı kendi oturumunda etkileyen genellikle kullanılan tooreport hello hatalardır.</span><span class="sxs-lookup"><span data-stu-id="59607-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="59607-171">İş hataları</span><span class="sxs-lookup"><span data-stu-id="59607-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-172">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="59607-173">Hataları olan yerine işi ilgili tooa olabilir ilgili toohello geçerli kullanıcı oturumunun.</span><span class="sxs-lookup"><span data-stu-id="59607-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-174">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="59607-175">Raporlama çökme (Crash)</span><span class="sxs-lookup"><span data-stu-id="59607-175">Reporting Crashes</span></span>
<span data-ttu-id="59607-176">Merhaba Aracısı çökme (Crash) ile iki yöntemleri toodeal sağlar.</span><span class="sxs-lookup"><span data-stu-id="59607-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="59607-177">Bir özel durum Gönder</span><span class="sxs-lookup"><span data-stu-id="59607-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-178">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="59607-179">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-179">Example</span></span>
<span data-ttu-id="59607-180">Bir özel durum herhangi bir zamanda çağırarak gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="59607-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="59607-181">Bir isteğe bağlı bir parametre tooterminate hello katılım oturumu sırasında hello kullanabilirsiniz hello kilitlenme gönderme daha aynı anda.</span><span class="sxs-lookup"><span data-stu-id="59607-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="59607-182">Bu nedenle, toodo arayın:</span><span class="sxs-lookup"><span data-stu-id="59607-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="59607-183">Bunu yaparsanız, hello oturum işleri hello kilitlenme gönderdikten sonra kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="59607-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="59607-184">İşlenmeyen bir özel durum Gönder</span><span class="sxs-lookup"><span data-stu-id="59607-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="59607-185">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="59607-186">Katılım yöntemi toosend işlenmeyen özel durumlar da sağlar.</span><span class="sxs-lookup"><span data-stu-id="59607-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="59607-187">Merhaba silverlight UnhandledException olay işleyicisinin içinden kullanıldığında bu özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="59607-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="59607-188">Bu yöntem olacak **her zaman** hello katılım oturum ve işleri adlı sonra sonlandırılacak.</span><span class="sxs-lookup"><span data-stu-id="59607-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="59607-189">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-189">Example</span></span>
<span data-ttu-id="59607-190">Tooimplement kullanın (özellikle, hello otomatik kilitlenme raporlama katılım özelliği devre dışı bıraktıysanız) kendi UnhandledException işleyicisi.</span><span class="sxs-lookup"><span data-stu-id="59607-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="59607-191">Örneğin, hello içinde `Application_UnhandledException` hello yöntemi `App.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="59607-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="59607-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="59607-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="59607-193">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="59607-194">Hello devre dışı olay tetiklenir sonra hello kullanıcı İleri, bir uygulama çıktığınızda gittiğinde hello işletim sistemi tooput Merhaba uygulaması etkinliği olmayan bir duruma deneyecek.</span><span class="sxs-lookup"><span data-stu-id="59607-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="59607-195">Ardından, kaldırıldı olarak işaretleme hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="59607-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="59607-196">Bu işlemde bir uygulama sonlandırıldı ancak hello uygulama ve her bir sayfayı hello hello uygulamadaki hello durumuyla ilgili bazı veriler korunur.</span><span class="sxs-lookup"><span data-stu-id="59607-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="59607-197">Tooinsert sahip `EngagementAgent.Instance.OnActivated(e)` hello içinde `Application_Activated` hello App.xaml.cs dosyasını tooreset hello katılım Merhaba uygulaması kaldırıldı kaldığında Aracısı yönteminden.</span><span class="sxs-lookup"><span data-stu-id="59607-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="59607-198">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="59607-199">Cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="59607-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="59607-200">Bu yöntemi çağrılarak hello engagement cihaz kimliğini elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59607-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="59607-201">Ek özellikler parametreleri</span><span class="sxs-lookup"><span data-stu-id="59607-201">Extras parameters</span></span>
<span data-ttu-id="59607-202">Rastgele veriler ekli tooan olay, bir hata, bir etkinlik veya bir iş olabilir.</span><span class="sxs-lookup"><span data-stu-id="59607-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="59607-203">Bu verilerin bir sözlüğünü kullanarak yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="59607-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="59607-204">Anahtarları ve değerleri herhangi bir türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="59607-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="59607-205">Bu nedenle tooinsert kendi türünde ek özellikler istiyorsanız, bu tür için bir veri sözleşmesi tooadd zorunda ek özellikler veri serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="59607-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="59607-206">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-206">Example</span></span>
<span data-ttu-id="59607-207">Yeni bir sınıf "Kişi" oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="59607-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="59607-208">Ardından, ekleyeceğiz bir `Person` örneği tooan ek.</span><span class="sxs-lookup"><span data-stu-id="59607-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="59607-209">Diğer nesne türlerini yerleştirirseniz, kendi ToString() yöntemini uygulanan tooreturn İnsan okunabilir dize olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="59607-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="59607-210">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="59607-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="59607-211">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="59607-211">Keys</span></span>
<span data-ttu-id="59607-212">Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="59607-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="59607-213">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="59607-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="59607-214">Boyut</span><span class="sxs-lookup"><span data-stu-id="59607-214">Size</span></span>
<span data-ttu-id="59607-215">Ek özellikler sınırlı çok**1024** çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="59607-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="59607-216">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="59607-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="59607-217">Başvuru</span><span class="sxs-lookup"><span data-stu-id="59607-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="59607-218">Merhaba SendAppInfo() işlevini kullanarak bilgi (veya diğer uygulama belirli bilgileri) izleme el ile bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59607-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="59607-219">Bu bilgi artımlı olarak gönderilebilir Not: yalnızca hello son değer belirli bir anahtar için belirli bir aygıt için korunur.</span><span class="sxs-lookup"><span data-stu-id="59607-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="59607-220">Olay ek özellikler gibi sözlük kullanma\<nesne, nesne\> tooattach bilgiler.</span><span class="sxs-lookup"><span data-stu-id="59607-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="59607-221">Örnek</span><span class="sxs-lookup"><span data-stu-id="59607-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="59607-222">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="59607-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="59607-223">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="59607-223">Keys</span></span>
<span data-ttu-id="59607-224">Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="59607-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="59607-225">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="59607-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="59607-226">Boyut</span><span class="sxs-lookup"><span data-stu-id="59607-226">Size</span></span>
<span data-ttu-id="59607-227">Uygulama bilgilerini sınırlı çok**1024** çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="59607-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="59607-228">Hello önceki hello toohello sunucu gönderilen JSON 44 karakter uzunluğunda örnektir:</span><span class="sxs-lookup"><span data-stu-id="59607-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="59607-229">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="59607-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="59607-230">Günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="59607-230">Enable Logging</span></span>
<span data-ttu-id="59607-231">Merhaba SDK hello IDE konsolunda yapılandırılmış tooproduce test günlüklerinin olabilir.</span><span class="sxs-lookup"><span data-stu-id="59607-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="59607-232">Bu günlükler varsayılan olarak etkinleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="59607-232">These logs are not activated by default.</span></span> <span data-ttu-id="59607-233">toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="59607-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
