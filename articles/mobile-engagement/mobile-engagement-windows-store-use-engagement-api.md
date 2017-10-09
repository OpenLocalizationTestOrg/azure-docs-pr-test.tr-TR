---
title: "aaaHow tooUse hello katılım API Windows Evrensel"
description: "Nasıl tooUse hello katılım API Windows Evrensel"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="3be8d-103">Nasıl tooUse hello katılım API Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="3be8d-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="3be8d-104">Bu belge bir eklenti toohello belgesidir [nasıl tooIntegrate Engagement Windows Evrensel üzerinde](mobile-engagement-windows-store-integrate-engagement.md): nasıl toouse hello katılım API tooreport uygulama istatistikleri hakkında derinliği ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="3be8d-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="3be8d-105">Yalnızca katılım tooreport uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgi istiyorsanız, ardından hello en basit yolu toomake tüm olduğunu aklınızda bulundurun, `Page` alt sınıfları devral hello `EngagementPage` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3be8d-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="3be8d-106">Daha fazla tooreport uygulama belirli olaylar, hatalar ve işleri gerekiyorsa örneğin toodo istiyorsanız veya tooreport uygulamanızın etkinlikleri farklı bir şekilde bir hello uygulanan hello daha varsa `EngagementPage` sınıfları yeniden toouse hello gerekiyor Katılım API.</span><span class="sxs-lookup"><span data-stu-id="3be8d-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="3be8d-107">Merhaba katılım API hello tarafından sağlanan `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3be8d-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="3be8d-108">Toothose yöntemlerle erişebilirsiniz `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="3be8d-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="3be8d-109">Merhaba aracı modülü başlatılmadı olsa bile, her çağrı toohello API ertelenir ve hello Aracısı kullanılabilir olduğunda yeniden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3be8d-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="3be8d-110">Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="3be8d-110">Engagement concepts</span></span>
<span data-ttu-id="3be8d-111">Merhaba aşağıdaki bölümleri İyileştir hello ortak [Mobile Engagement kavramları](mobile-engagement-concepts.md) hello Evrensel Windows platformu için.</span><span class="sxs-lookup"><span data-stu-id="3be8d-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="3be8d-112">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="3be8d-112">`Session` and `Activity`</span></span>
<span data-ttu-id="3be8d-113">Bir *etkinlik* genellikle toosay hello hello uygulama, bir sayfayla ilişkili *etkinlik* hello sayfası görüntülenir ve hello sayfa kapatıldığında durdurduğunda başlatır: hello hello zaman böyledir Engagement SDK'sı tümleşik hello kullanarak `EngagementPage` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3be8d-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="3be8d-114">Ancak *etkinlikleri* de el ile Merhaba katılım API kullanılarak denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="3be8d-115">Bu, belirli bir sayfa çeşitli alt bölümleri tooget (örneğin tooknow ne sıklıkta ve ne kadar süre içinde bu sayfa iletişim kutuları kullanılır), bu sayfanın hello kullanımı hakkında daha fazla ayrıntı toosplit sağlar.</span><span class="sxs-lookup"><span data-stu-id="3be8d-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="3be8d-116">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="3be8d-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="3be8d-117">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="3be8d-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-118">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-119">Toocall gerek `StartActivity()` her zaman hello kullanıcı etkinliği değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="3be8d-120">Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="3be8d-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3be8d-121">Merhaba uygulama kapatıldığında hello SDK otomatik olarak hello EndActivity yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3be8d-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="3be8d-122">Bu nedenle, toocall hello StartActivity yöntemi hello kullanıcı hello etkinliğini değiştirir ve hello EndActivity yöntemi, bu yöntemi çağırmadan itibaren hello geçerli oturum toobe zorlar tooNEVER çağrısı sona erdi önerilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="3be8d-123">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="3be8d-124">Kullanıcı kendi geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="3be8d-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-125">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="3be8d-126">Bu başlangıç etkinliği ve hello oturumu sona erer.</span><span class="sxs-lookup"><span data-stu-id="3be8d-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="3be8d-127">Gerçekleştirmekte olduğunuz gerçekten bilmiyorsanız bu yöntem çağırmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="3be8d-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-128">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="3be8d-129">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="3be8d-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="3be8d-130">Bir işi Başlat</span><span class="sxs-lookup"><span data-stu-id="3be8d-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-131">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-132">Bir süre boyunca hello iş tootrack bazı görevleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3be8d-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-133">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="3be8d-134">Bir işin bitiş</span><span class="sxs-lookup"><span data-stu-id="3be8d-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-135">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="3be8d-136">Bir iş tarafından izlenen bir görev sonlandırıldı hemen hello iş adı sağlayarak bu proje için hello EndJob yöntemini çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3be8d-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="3be8d-138">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="3be8d-138">Reporting Events</span></span>
<span data-ttu-id="3be8d-139">Üç tür olay vardır:</span><span class="sxs-lookup"><span data-stu-id="3be8d-139">There is three types of events :</span></span>

* <span data-ttu-id="3be8d-140">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="3be8d-140">Standalone events</span></span>
* <span data-ttu-id="3be8d-141">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="3be8d-141">Session events</span></span>
* <span data-ttu-id="3be8d-142">İş olayları</span><span class="sxs-lookup"><span data-stu-id="3be8d-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="3be8d-143">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="3be8d-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-144">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-145">Tek başına olaylar oturumu hello bağlamı dışında gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="3be8d-147">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="3be8d-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-148">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-149">Oturum, kendi oturumunda bir kullanıcı tarafından gerçekleştirilen genellikle kullanılan tooreport hello Eylemler olaylardır.</span><span class="sxs-lookup"><span data-stu-id="3be8d-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-150">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-150">Example</span></span>
<span data-ttu-id="3be8d-151">**Veri olmadan:**</span><span class="sxs-lookup"><span data-stu-id="3be8d-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="3be8d-152">**Verilerle:**</span><span class="sxs-lookup"><span data-stu-id="3be8d-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="3be8d-153">İş olayları</span><span class="sxs-lookup"><span data-stu-id="3be8d-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-154">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-155">İş, bir kullanıcı tarafından gerçekleştirilen işi sırasında genellikle kullanılan tooreport hello Eylemler olaylardır.</span><span class="sxs-lookup"><span data-stu-id="3be8d-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-156">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="3be8d-157">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="3be8d-157">Reporting Errors</span></span>
<span data-ttu-id="3be8d-158">Üç tür hataları vardır:</span><span class="sxs-lookup"><span data-stu-id="3be8d-158">There are three types of errors :</span></span>

* <span data-ttu-id="3be8d-159">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="3be8d-159">Standalone errors</span></span>
* <span data-ttu-id="3be8d-160">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="3be8d-160">Session errors</span></span>
* <span data-ttu-id="3be8d-161">İş hataları</span><span class="sxs-lookup"><span data-stu-id="3be8d-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="3be8d-162">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="3be8d-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-163">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-164">Bulmadýðýný toosession hataları, bir oturum Merhaba içeriğine dışında tek başına hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-165">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="3be8d-166">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="3be8d-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-167">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-168">Oturum hatalar hello kullanıcı kendi oturumunda etkileyen genellikle kullanılan tooreport hello hatalardır.</span><span class="sxs-lookup"><span data-stu-id="3be8d-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-169">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="3be8d-170">İş hataları</span><span class="sxs-lookup"><span data-stu-id="3be8d-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-171">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="3be8d-172">Hataları olan yerine işi ilgili tooa olabilir ilgili toohello geçerli kullanıcı oturumunun.</span><span class="sxs-lookup"><span data-stu-id="3be8d-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-173">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="3be8d-174">Raporlama çökme (Crash)</span><span class="sxs-lookup"><span data-stu-id="3be8d-174">Reporting Crashes</span></span>
<span data-ttu-id="3be8d-175">Merhaba Aracısı çökme (Crash) ile iki yöntemleri toodeal sağlar.</span><span class="sxs-lookup"><span data-stu-id="3be8d-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="3be8d-176">Bir özel durum Gönder</span><span class="sxs-lookup"><span data-stu-id="3be8d-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-177">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="3be8d-178">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-178">Example</span></span>
<span data-ttu-id="3be8d-179">Bir özel durum herhangi bir zamanda çağırarak gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3be8d-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="3be8d-180">Bir isteğe bağlı bir parametre tooterminate hello katılım oturumu sırasında hello kullanabilirsiniz hello kilitlenme gönderme daha aynı anda.</span><span class="sxs-lookup"><span data-stu-id="3be8d-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="3be8d-181">Bu nedenle, toodo arayın:</span><span class="sxs-lookup"><span data-stu-id="3be8d-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="3be8d-182">Bunu yaparsanız, hello oturum işleri hello kilitlenme gönderdikten sonra kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="3be8d-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="3be8d-183">İşlenmeyen bir özel durum Gönder</span><span class="sxs-lookup"><span data-stu-id="3be8d-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="3be8d-184">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="3be8d-185">Katılım varsa yöntemi toosend işlenmeyen özel durumlar da sağlar **devre dışı** katılım otomatik **kilitlenme** raporlama.</span><span class="sxs-lookup"><span data-stu-id="3be8d-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="3be8d-186">Merhaba uygulama UnhandledException olay işleyicisinin içinden kullanıldığında bu özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="3be8d-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="3be8d-187">Bu yöntem olacak **her zaman** hello katılım oturum ve işleri adlı sonra sonlandırılacak.</span><span class="sxs-lookup"><span data-stu-id="3be8d-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="3be8d-188">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-188">Example</span></span>
<span data-ttu-id="3be8d-189">Tooimplement kullanmak, kendi UnhandledExceptionEventArgs işleyicisi.</span><span class="sxs-lookup"><span data-stu-id="3be8d-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="3be8d-190">Örneğin, hello ekleyin `Current_UnhandledException` hello yöntemi `App.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="3be8d-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="3be8d-191">App.xaml.cs dosyasında "Ortak App() {}" ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3be8d-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="3be8d-192">Cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="3be8d-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="3be8d-193">Bu yöntemi çağrılarak hello engagement cihaz kimliğini elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3be8d-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="3be8d-194">Ek özellikler parametreleri</span><span class="sxs-lookup"><span data-stu-id="3be8d-194">Extras parameters</span></span>
<span data-ttu-id="3be8d-195">Rastgele veriler ekli tooan olay, bir hata, bir etkinlik veya bir iş olabilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="3be8d-196">Bu verilerin bir sözlüğünü kullanarak yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="3be8d-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="3be8d-197">Anahtarları ve değerleri herhangi bir türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="3be8d-198">Bu nedenle tooinsert kendi türünde ek özellikler istiyorsanız, bu tür için bir veri sözleşmesi tooadd zorunda ek özellikler veri serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="3be8d-199">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-199">Example</span></span>
<span data-ttu-id="3be8d-200">Yeni bir sınıf "Kişi" oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="3be8d-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="3be8d-201">Ardından, ekleyeceğiz bir `Person` örneği tooan ek.</span><span class="sxs-lookup"><span data-stu-id="3be8d-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="3be8d-202">Diğer nesne türlerini yerleştirirseniz, kendi ToString() yöntemini uygulanan tooreturn İnsan okunabilir dize olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3be8d-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="3be8d-203">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="3be8d-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3be8d-204">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="3be8d-204">Keys</span></span>
<span data-ttu-id="3be8d-205">Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3be8d-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="3be8d-206">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="3be8d-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3be8d-207">Boyut</span><span class="sxs-lookup"><span data-stu-id="3be8d-207">Size</span></span>
<span data-ttu-id="3be8d-208">Ek özellikler sınırlı çok**1024** çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="3be8d-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="3be8d-209">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="3be8d-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="3be8d-210">Başvuru</span><span class="sxs-lookup"><span data-stu-id="3be8d-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="3be8d-211">Merhaba SendAppInfo() işlevini kullanarak bilgi (veya diğer uygulama belirli bilgileri) izleme el ile bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3be8d-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="3be8d-212">Bu verileri artımlı olarak gönderilebilir Not: yalnızca hello son değer belirli bir anahtar için belirli bir aygıt için korunur.</span><span class="sxs-lookup"><span data-stu-id="3be8d-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="3be8d-213">Olay ek özellikler gibi sözlük kullanma\<nesne, nesne\> tooattach veri.</span><span class="sxs-lookup"><span data-stu-id="3be8d-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="3be8d-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="3be8d-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="3be8d-215">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="3be8d-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3be8d-216">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="3be8d-216">Keys</span></span>
<span data-ttu-id="3be8d-217">Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3be8d-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="3be8d-218">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="3be8d-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3be8d-219">Boyut</span><span class="sxs-lookup"><span data-stu-id="3be8d-219">Size</span></span>
<span data-ttu-id="3be8d-220">Uygulama bilgilerini sınırlı çok**1024** çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="3be8d-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="3be8d-221">Hello önceki hello toohello sunucu gönderilen JSON 44 karakter uzunluğunda örnektir:</span><span class="sxs-lookup"><span data-stu-id="3be8d-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="3be8d-222">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="3be8d-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="3be8d-223">Günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3be8d-223">Enable Logging</span></span>
<span data-ttu-id="3be8d-224">Merhaba SDK hello IDE konsolunda yapılandırılmış tooproduce test günlüklerinin olabilir.</span><span class="sxs-lookup"><span data-stu-id="3be8d-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="3be8d-225">Bu günlükler varsayılan olarak etkinleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="3be8d-225">These logs are not activated by default.</span></span> <span data-ttu-id="3be8d-226">toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="3be8d-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

