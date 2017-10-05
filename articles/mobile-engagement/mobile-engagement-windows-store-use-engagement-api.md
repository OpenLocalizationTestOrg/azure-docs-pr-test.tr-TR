---
title: API Engagement Windows Evrensel kullanma
description: API Engagement Windows Evrensel kullanma
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
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="21f41-103">API Engagement Windows Evrensel kullanma</span><span class="sxs-lookup"><span data-stu-id="21f41-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="21f41-104">Bu belge belgeye bir eklentidir [tümleştirmek Engagement Windows Evrensel üzerinde nasıl](mobile-engagement-windows-store-integrate-engagement.md): katılım API uygulama istatistikleri rapor için nasıl kullanılacağı hakkında derinliği ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f41-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="21f41-105">Uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgileri raporlamak için katılım yalnızca istiyorsanız, sonra en basit yolu tüm olduğunu aklınızda bulundurun, `Page` alt sınıfları `EngagementPage` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21f41-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="21f41-106">Daha fazla bilgi için uygulama belirli olaylar, hatalar ve işleri, rapor gerekiyorsa örnek yapmak istiyorsanız veya uygulamanızın etkinlikleri uygulanan bir daha farklı bir şekilde bildirmek varsa `EngagementPage` sınıfları yeniden katılım API'sini kullanmanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="21f41-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="21f41-107">Katılım API'si tarafından sağlanan `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21f41-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="21f41-108">Bu yöntemlerle erişebilirsiniz `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="21f41-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="21f41-109">Aracı modülü başlatılmadı olsa bile, her API çağrısı ertelenir ve aracı kullanılabilir olduğunda yeniden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="21f41-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="21f41-110">Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="21f41-110">Engagement concepts</span></span>
<span data-ttu-id="21f41-111">Aşağıdaki bölümleri yaygın İyileştir [Mobile Engagement kavramları](mobile-engagement-concepts.md) Evrensel Windows platformu için.</span><span class="sxs-lookup"><span data-stu-id="21f41-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="21f41-112">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="21f41-112">`Session` and `Activity`</span></span>
<span data-ttu-id="21f41-113">Bir *etkinlik* yani genellikle uygulama bir sayfayla ilişkilendirilen *etkinlik* sayfası görüntülenir ve sayfa kapatıldığında durdurduğunda başlatır: Engagement SDK'sını kullanarak tümleştirildiğinde bu durumda `EngagementPage` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21f41-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="21f41-114">Ancak *etkinlikleri* de el ile katılım API'si kullanılarak denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="21f41-115">Bu, belirli bir sayfa (örneğin ne sıklıkta ve ne kadar süreyle iletişim kutuları bu sayfa içinde kullanılan bilmeniz) bu sayfanın kullanımı hakkında daha fazla bilgi almak için birkaç alt bölümlerinde bölmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f41-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="21f41-116">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="21f41-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="21f41-117">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="21f41-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-118">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-119">Çağırmanız gerekir `StartActivity()` kullanıcı etkinliği değişiklikleri her zaman.</span><span class="sxs-lookup"><span data-stu-id="21f41-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="21f41-120">Bu işlev ilk çağrıda yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="21f41-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21f41-121">Uygulama kapatıldığında SDK'yı otomatik olarak EndActivity yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="21f41-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="21f41-122">Bu nedenle, kullanıcı değişiklikleri ve hiçbir zaman etkinliği çağrı her EndActivity yöntemi bu yöntemi çağırmadan sonlandırılmak üzere geçerli oturumdaki zorlar beri StartActivity yöntemini çağırmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="21f41-123">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="21f41-124">Kullanıcı kendi geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="21f41-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-125">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="21f41-126">Bu etkinliği ve oturum sona erer.</span><span class="sxs-lookup"><span data-stu-id="21f41-126">This ends the activity and the session.</span></span> <span data-ttu-id="21f41-127">Gerçekleştirmekte olduğunuz gerçekten bilmiyorsanız bu yöntem çağırmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="21f41-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-128">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="21f41-129">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="21f41-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="21f41-130">Bir işi Başlat</span><span class="sxs-lookup"><span data-stu-id="21f41-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-131">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-132">İş, bir süre boyunca bazı görevleri izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f41-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-133">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="21f41-134">Bir işin bitiş</span><span class="sxs-lookup"><span data-stu-id="21f41-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-135">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="21f41-136">Bir iş tarafından izlenen bir görev sonlandırıldı hemen iş adı sağlayarak bu proje için EndJob yöntemi çağırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f41-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="21f41-138">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="21f41-138">Reporting Events</span></span>
<span data-ttu-id="21f41-139">Üç tür olay vardır:</span><span class="sxs-lookup"><span data-stu-id="21f41-139">There is three types of events :</span></span>

* <span data-ttu-id="21f41-140">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="21f41-140">Standalone events</span></span>
* <span data-ttu-id="21f41-141">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="21f41-141">Session events</span></span>
* <span data-ttu-id="21f41-142">İş olayları</span><span class="sxs-lookup"><span data-stu-id="21f41-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="21f41-143">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="21f41-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-144">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-145">Tek başına olaylar oturum bağlamı dışında gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="21f41-147">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="21f41-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-148">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-149">Oturum olaylar, genellikle kendi oturumu sırasında bir kullanıcı tarafından gerçekleştirilen eylemleri bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f41-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-150">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-150">Example</span></span>
<span data-ttu-id="21f41-151">**Veri olmadan:**</span><span class="sxs-lookup"><span data-stu-id="21f41-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="21f41-152">**Verilerle:**</span><span class="sxs-lookup"><span data-stu-id="21f41-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="21f41-153">İş olayları</span><span class="sxs-lookup"><span data-stu-id="21f41-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-154">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-155">İş olaylar, genellikle bir işi sırasında bir kullanıcı tarafından gerçekleştirilen eylemleri bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f41-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-156">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="21f41-157">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="21f41-157">Reporting Errors</span></span>
<span data-ttu-id="21f41-158">Üç tür hataları vardır:</span><span class="sxs-lookup"><span data-stu-id="21f41-158">There are three types of errors :</span></span>

* <span data-ttu-id="21f41-159">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="21f41-159">Standalone errors</span></span>
* <span data-ttu-id="21f41-160">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="21f41-160">Session errors</span></span>
* <span data-ttu-id="21f41-161">İş hataları</span><span class="sxs-lookup"><span data-stu-id="21f41-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="21f41-162">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="21f41-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-163">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-164">Oturum hataları aykırı bir oturum bağlamı dışında tek başına hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-165">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="21f41-166">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="21f41-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-167">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-168">Oturum hatalar genellikle kendi oturumu sırasında kullanıcı etkileyen hatalarını bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f41-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-169">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="21f41-170">İş hataları</span><span class="sxs-lookup"><span data-stu-id="21f41-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-171">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="21f41-172">Geçerli kullanıcı oturumuyla ilgili yerine çalıştırılan bir iş hataları ile ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-173">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="21f41-174">Raporlama çökme (Crash)</span><span class="sxs-lookup"><span data-stu-id="21f41-174">Reporting Crashes</span></span>
<span data-ttu-id="21f41-175">Aracı çökme (Crash) ile mücadele etmek için iki yöntem sunar.</span><span class="sxs-lookup"><span data-stu-id="21f41-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="21f41-176">Bir özel durum Gönder</span><span class="sxs-lookup"><span data-stu-id="21f41-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-177">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="21f41-178">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-178">Example</span></span>
<span data-ttu-id="21f41-179">Bir özel durum herhangi bir zamanda çağırarak gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21f41-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="21f41-180">İsteğe bağlı parametresi, kilitlenme gönderme daha aynı anda katılım oturumu sona erdirmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f41-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="21f41-181">Bunu yapmak için arayın:</span><span class="sxs-lookup"><span data-stu-id="21f41-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="21f41-182">Bunu yaparsanız, oturum ve işleri kilitlenme gönderdikten sonra kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="21f41-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="21f41-183">İşlenmeyen bir özel durum Gönder</span><span class="sxs-lookup"><span data-stu-id="21f41-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="21f41-184">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="21f41-185">Katılım ayrıca işlenmeyen özel durumlar varsa göndermek üzere bir yöntem sağlar **devre dışı** katılım otomatik **kilitlenme** raporlama.</span><span class="sxs-lookup"><span data-stu-id="21f41-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="21f41-186">Uygulama UnhandledException olay işleyicisinin içinden kullanıldığında bu özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f41-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="21f41-187">Bu yöntem olacak **her zaman** adlı sonra işler ve katılım oturum sonlandırılacak.</span><span class="sxs-lookup"><span data-stu-id="21f41-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="21f41-188">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-188">Example</span></span>
<span data-ttu-id="21f41-189">Kendi UnhandledExceptionEventArgs işleyici uygulamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f41-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="21f41-190">Örneğin, ekleyin `Current_UnhandledException` yöntemi `App.xaml.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="21f41-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="21f41-191">App.xaml.cs dosyasında "Ortak App() {}" ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21f41-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="21f41-192">Cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="21f41-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="21f41-193">Bu yöntemi çağrılarak engagement cihaz kimliğini elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f41-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="21f41-194">Ek özellikler parametreleri</span><span class="sxs-lookup"><span data-stu-id="21f41-194">Extras parameters</span></span>
<span data-ttu-id="21f41-195">Rastgele veriler, bir olay, bir hata, bir etkinlik veya bir iş için eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="21f41-196">Bu verilerin bir sözlüğünü kullanarak yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="21f41-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="21f41-197">Anahtarları ve değerleri herhangi bir türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="21f41-198">Bu tür için bir veri sözleşmesi eklemek zorunda ek özellikler kendi türü eklemek istiyorsanız şekilde ek özellikler veri serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="21f41-199">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-199">Example</span></span>
<span data-ttu-id="21f41-200">Yeni bir sınıf "Kişi" oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="21f41-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="21f41-201">Ardından, ekleyeceğiz bir `Person` fazladan örneğine.</span><span class="sxs-lookup"><span data-stu-id="21f41-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="21f41-202">Diğer nesne türlerini yerleştirirseniz, kendi ToString() yöntemini İnsan okunabilir dize döndürecek şekilde uygulanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="21f41-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="21f41-203">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="21f41-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="21f41-204">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="21f41-204">Keys</span></span>
<span data-ttu-id="21f41-205">Nesne tablosundaki her anahtarın şu normal ifadeyle aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f41-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="21f41-206">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="21f41-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="21f41-207">Boyut</span><span class="sxs-lookup"><span data-stu-id="21f41-207">Size</span></span>
<span data-ttu-id="21f41-208">Ek özellikler sınırlı **1024** çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="21f41-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="21f41-209">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="21f41-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="21f41-210">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21f41-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="21f41-211">El ile SendAppInfo() kullanarak bilgi (veya diğer uygulama belirli bilgileri) izleme işlevini bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f41-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="21f41-212">Bu verileri artımlı olarak gönderilebilir Not: belirli bir aygıt için belirli bir anahtar için yalnızca en son değeri korunur.</span><span class="sxs-lookup"><span data-stu-id="21f41-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="21f41-213">Olay ek özellikler gibi sözlük kullanma\<nesne, nesne\> veri eklemek için.</span><span class="sxs-lookup"><span data-stu-id="21f41-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="21f41-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f41-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="21f41-215">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="21f41-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="21f41-216">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="21f41-216">Keys</span></span>
<span data-ttu-id="21f41-217">Nesne tablosundaki her anahtarın şu normal ifadeyle aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f41-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="21f41-218">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="21f41-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="21f41-219">Boyut</span><span class="sxs-lookup"><span data-stu-id="21f41-219">Size</span></span>
<span data-ttu-id="21f41-220">Uygulama bilgilerini sınırlıdır **1024** çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="21f41-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="21f41-221">Önceki örnekte, sunucuya gönderilen JSON 44 karakter olacak:</span><span class="sxs-lookup"><span data-stu-id="21f41-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="21f41-222">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="21f41-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="21f41-223">Günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="21f41-223">Enable Logging</span></span>
<span data-ttu-id="21f41-224">SDK, test günlüklerinin IDE konsolunda üretmek için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f41-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="21f41-225">Bu günlükler varsayılan olarak etkinleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="21f41-225">These logs are not activated by default.</span></span> <span data-ttu-id="21f41-226">Bu özelleştirmek için özellik güncelleştirme `EngagementAgent.Instance.TestLogEnabled` bulunan değer birine `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="21f41-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

