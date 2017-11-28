---
title: "Scheduler kavramları, terimleri ve varlıkları | Microsoft Belgeleri"
description: "İşler ve iş koleksiyonları dahil Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi.  Zamanlanan bir işin kapsamlı bir örneği gösterilmektedir."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="8ffc9-104">Scheduler kavramları ve terminolojisi + varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="8ffc9-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="8ffc9-105">Scheduler varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="8ffc9-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="8ffc9-106">Aşağıdaki tabloda Scheduler API’si tarafından gösterilen ya da kullanılan ana kaynaklar açıklanır:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="8ffc9-107">Kaynak</span><span class="sxs-lookup"><span data-stu-id="8ffc9-107">Resource</span></span> | <span data-ttu-id="8ffc9-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ffc9-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ffc9-109">**İş koleksiyonu**</span><span class="sxs-lookup"><span data-stu-id="8ffc9-109">**Job collection**</span></span> |<span data-ttu-id="8ffc9-110">İş koleksiyonu, bir grup işi içerir ve koleksiyondaki işler tarafından paylaşılan ayarlar, kotalar ve kısıtlamaları tutar.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="8ffc9-111">İş koleksiyonu abonelik sahibi tarafından oluşturulur ve işleri kullanım veya uygulama sınırlarına göre gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="8ffc9-112">Tek bir bölge için kısıtlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-112">It’s constrained to one region.</span></span> <span data-ttu-id="8ffc9-113">Ayrıca, bu koleksiyondaki tüm işlerin kullanımını kısıtlamak için kotaları da uygulamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="8ffc9-114">Kotalar MaxJobs ve MaxRecurrence değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="8ffc9-115">**İş**</span><span class="sxs-lookup"><span data-stu-id="8ffc9-115">**Job**</span></span> |<span data-ttu-id="8ffc9-116">Bir iş, yürütmek üzere basit ya da karmaşık stratejilerle tek bir yinelenen eylemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="8ffc9-117">Eylemler HTTP, depolama kuyruğu, hizmet veri yolu kuyruğu ya da hizmet veri yolu konusu isteklerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="8ffc9-118">**İş geçmişi**</span><span class="sxs-lookup"><span data-stu-id="8ffc9-118">**Job history**</span></span> |<span data-ttu-id="8ffc9-119">İş geçmişi bir işin yürütülmesine ilişkin ayrıntılarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="8ffc9-120">Bu başarılı ve hatalı karşılaştırmasının yanı sıra tüm yanıt ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="8ffc9-121">Scheduler varlık yönetimi</span><span class="sxs-lookup"><span data-stu-id="8ffc9-121">Scheduler entity management</span></span>
<span data-ttu-id="8ffc9-122">Yüksek düzeyde, scheduler ve hizmet yönetimi API’si kaynaklarda aşağıdaki işlemleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="8ffc9-123">Özellik</span><span class="sxs-lookup"><span data-stu-id="8ffc9-123">Capability</span></span> | <span data-ttu-id="8ffc9-124">Açıklama ve URI adresi</span><span class="sxs-lookup"><span data-stu-id="8ffc9-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="8ffc9-125">**İş koleksiyonu yönetimi**</span><span class="sxs-lookup"><span data-stu-id="8ffc9-125">**Job collection management**</span></span> |<span data-ttu-id="8ffc9-126">İş koleksiyonları ve burada yer alan işleri oluşturma ve değiştirmeye yönelik AL, KOY ve SİL desteği.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="8ffc9-127">İş koleksiyonu, kotalar ve paylaşılan ayarlara yönelik işler ve eşlemeler için kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="8ffc9-128">İleride açıklanan kota örnekleri, maksimum iş sayısı ve en küçük yineleme aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="8ffc9-129">KOY ve SİL: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="8ffc9-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="8ffc9-130">AL: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="8ffc9-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="8ffc9-131">**İş yönetimi**</span><span class="sxs-lookup"><span data-stu-id="8ffc9-131">**Job management**</span></span> |<span data-ttu-id="8ffc9-132">İşleri oluşturma ve değiştirmeye yönelik AL, KOY, YAYIMLA, DÜZELTME EKİ UYGULA ve SİL desteği.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="8ffc9-133">Açık oluşturma olmaması için, tüm işler önceden mevcut bir iş koleksiyonuna ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="8ffc9-134">**İş geçmişi yönetimi**</span><span class="sxs-lookup"><span data-stu-id="8ffc9-134">**Job history management**</span></span> |<span data-ttu-id="8ffc9-135">İş geçen süresi ve iş yürütme sonuçları gibi, 60 günlük iş yürütme geçmişi getirmek üzere AL desteği.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="8ffc9-136">Durum ve duruma göre filtreleme için sorgu dizesi parametresi desteği ekler.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="8ffc9-137">İş türleri</span><span class="sxs-lookup"><span data-stu-id="8ffc9-137">Job types</span></span>
<span data-ttu-id="8ffc9-138">Birden çok iş türü vardır: HTTP işleri (SSL destekleyen HTTPS işleri dahil), depolama kuyruğu işleri, hizmet veri yolu kuyruğu işleri ve hizmet veri yolu konusu işleri.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="8ffc9-139">HTTP işleri, mevcut bir iş yükünde ya da hizmette uç noktaya sahipseniz idealdir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="8ffc9-140">Bu işleri depolama kuyrukları kullanan iş yükleri için ideal olacağından, depolama kuyruğu işlerini depolama kuyruklarında ileti yayımlamakta kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="8ffc9-141">Benzer şekilde, hizmet veri yolu işleri hizmet veri yolu kuyrukları ve konuları kullanan iş yükleri için idealdir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="8ffc9-142">Ayrıntılı "job" varlığı</span><span class="sxs-lookup"><span data-stu-id="8ffc9-142">The "job" entity in detail</span></span>
<span data-ttu-id="8ffc9-143">Temel düzeyde, zamanlanan bir iş birkaç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="8ffc9-144">İş zamanlayıcı başlatıldığında gerçekleştirilecek iş</span><span class="sxs-lookup"><span data-stu-id="8ffc9-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="8ffc9-145">(İsteğe bağlı) İşin çalıştırma süresi</span><span class="sxs-lookup"><span data-stu-id="8ffc9-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="8ffc9-146">(İsteğe bağlı) İşin ne zaman ve ne sıklıkta tekrarlanacağı</span><span class="sxs-lookup"><span data-stu-id="8ffc9-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="8ffc9-147">(İsteğe bağlı) Birincil eylem başarısız olursa tetiklenecek eylem</span><span class="sxs-lookup"><span data-stu-id="8ffc9-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="8ffc9-148">Dahili olarak, zamanlanan bir iş ayrıca sonraki zamanlanan yürütme zamanı gibi sistem tarafından sağlanan verileri de içerir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="8ffc9-149">Aşağıdaki kodda zamanlanan bir işin kapsamlı örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="8ffc9-150">Ayrıntılar sonraki bölümlerde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="8ffc9-151">Yukarıdaki örnek zamanlanan işte görülüğü gibi, bir iş tanımı birkaç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="8ffc9-152">Başlangıç zamanı ("startTime")</span><span class="sxs-lookup"><span data-stu-id="8ffc9-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="8ffc9-153">Hata eylemi ("errorAction") içeren eylem ("eylem")</span><span class="sxs-lookup"><span data-stu-id="8ffc9-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="8ffc9-154">Yineleme ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="8ffc9-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="8ffc9-155">Durum ("state")</span><span class="sxs-lookup"><span data-stu-id="8ffc9-155">State (“state”)</span></span>  
* <span data-ttu-id="8ffc9-156">Durum ("status")</span><span class="sxs-lookup"><span data-stu-id="8ffc9-156">Status (“status”)</span></span>  
* <span data-ttu-id="8ffc9-157">Yeniden deneme ilkesi ("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="8ffc9-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="8ffc9-158">Şimdi bunların her birini ayrıntılı inceleyelim:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="8ffc9-159">startTime</span><span class="sxs-lookup"><span data-stu-id="8ffc9-159">startTime</span></span>
<span data-ttu-id="8ffc9-160">"startTime" başlangıç zamanıdır ve arayanın hat üzerinde [ISO 8601 biçiminde](http://en.wikipedia.org/wiki/ISO_8601) bir saat dilimi farkı belirtmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="8ffc9-161">action ve errorAction</span><span class="sxs-lookup"><span data-stu-id="8ffc9-161">action and errorAction</span></span>
<span data-ttu-id="8ffc9-162">“action” her meydana gelişte çağrılan eylemdir ve hizmet başlatma türünü açıklar.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="8ffc9-163">Eylem, sağlanan zamanlamadan yürütülecek olan şeydir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="8ffc9-164">Scheduler, HTTP, depolama kuyruğu, hizmet veri yolu konusu ve hizmet veri yolu kuyruğu eylemlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="8ffc9-165">Yukarıdaki örnekteki eylem bir HTTP eylemidir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="8ffc9-166">Bir depolama kuyruğu eylemi örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="8ffc9-167">Bir hizmet veri yolu konusu eylemi örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="8ffc9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="8ffc9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="8ffc9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="8ffc9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="8ffc9-170">Bir hizmet veri yolu kuyruğu eylemi örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="8ffc9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="8ffc9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="8ffc9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // netMessaging ya da AMQP olabilir "authentication": {</span><span class="sxs-lookup"><span data-stu-id="8ffc9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="8ffc9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="8ffc9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="8ffc9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="8ffc9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="8ffc9-175">"errorAction", birincil eylem başarısız olduğunda çağrılan hata işleyicidir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="8ffc9-176">Bu değişkeni bir hata işleme uç noktasını çağırmak ya da kullanıcı bildirimi göndermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="8ffc9-177">Bu, birincilin kullanılabilir olmaması durumunda (örneğin, uç nokta sitesinde olağanüstü durum halinde) ikincil uç noktaya erişim için veya bir hata işleme uç noktasını bildirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="8ffc9-178">Birincil eylemde olduğu gibi, hata eylemi diğer eylemler temelinde basit ya da birleşik mantıklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="8ffc9-179">SAS belirteci oluşturmayı öğrenmek için bkz. [Paylaşılan Erişim İmzası Oluşturma ve Kullanma](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ffc9-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="8ffc9-180">yineleme</span><span class="sxs-lookup"><span data-stu-id="8ffc9-180">recurrence</span></span>
<span data-ttu-id="8ffc9-181">Yineleme birkaç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="8ffc9-182">Sıklık: Dakika, saat, gün, hafta, ay, yıldan biri</span><span class="sxs-lookup"><span data-stu-id="8ffc9-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="8ffc9-183">Aralık: Yineleme için belirlenen sıklıktaki aralık</span><span class="sxs-lookup"><span data-stu-id="8ffc9-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="8ffc9-184">Belirtilen zamanlama: Yinelemeye ilişkin dakika, saat, hafta içi günü, ay ve ayın günü değerlerini belirtin</span><span class="sxs-lookup"><span data-stu-id="8ffc9-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="8ffc9-185">Sayı: Yineleme sayısı</span><span class="sxs-lookup"><span data-stu-id="8ffc9-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="8ffc9-186">Bitiş zamanı: Belirtilen bitiş zamanından sonra hiç bir iş yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="8ffc9-187">Bir iş, JSON tanımında belirtilen yinelenen nesneye sahipse yinelenendir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="8ffc9-188">Sayı ve endTime belirtilmişse, önce meydana gelen tamamlama kuralı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="8ffc9-189">durum</span><span class="sxs-lookup"><span data-stu-id="8ffc9-189">state</span></span>
<span data-ttu-id="8ffc9-190">İşin durumu dört değerden biridir: etkin, devre dışı, tamamlandı ya da hatalı.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="8ffc9-191">Etkin ya da devre dışı durumuna güncelleştirmek amacıyla işleri KOYABİLİR ya da DÜZELTME EKİ UYGULAYABİLİRSİNİZ.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="8ffc9-192">Bir işin durumu tamamlandı ya da hatalı ise, bu güncelleştirilemeyecek son aşamadır (iş yine de SİLİNEBİLİR)</span><span class="sxs-lookup"><span data-stu-id="8ffc9-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="8ffc9-193">Durum özelliğinin bir örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8ffc9-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="8ffc9-194">Tamamlanan ve hatalı işler 60 gün sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="8ffc9-195">durum</span><span class="sxs-lookup"><span data-stu-id="8ffc9-195">status</span></span>
<span data-ttu-id="8ffc9-196">Scheduler işi başladıktan sonra, işin geçerli durumu hakkında bilgi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="8ffc9-197">Bu nesne kullanıcı tarafından ayarlanamaz— sistem tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="8ffc9-198">Ancak, bir kimsenin işin durumunu kolayca edinebileceği şekilde iş nesnesinde yer alır (ayrı bağlantılı bir kaynak yerine).</span><span class="sxs-lookup"><span data-stu-id="8ffc9-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="8ffc9-199">İş durumu, önceki yürütme saatini (varsa), sonraki zamanlanan yürütmeyi (devam eden işler için) ve iş yürütme sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="8ffc9-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="8ffc9-200">retryPolicy</span></span>
<span data-ttu-id="8ffc9-201">Scheduler işi başarısız olursa, eylemin yeniden denenip denenmeyeceğini ve bunun nasıl yapılacağını belirlemek için bir yeniden deneme ilkesi belirlemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="8ffc9-202">Bu **retryType** nesnesi tarafından belirlenir; yukarıda gösterildiği gibi yeniden deneme ilkesi yoksa, **yok** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="8ffc9-203">Yeniden deneme ilkesi varsa, **sabit** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="8ffc9-204">Bir yeniden deneme ilkesi ayarlamak için iki ek ayar belirtilebilir: yeniden deneme aralığı (**retryInterval**) ve yeniden deneme sayısı (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="8ffc9-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="8ffc9-205">**retryInterval** nesnesi ile belirtilen yeniden deneme aralığı, yeniden denemeler arasındaki aralıktır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="8ffc9-206">Varsayılan değer 30 saniye, minimum yapılandırılabilir değeri 15 saniye, ve maksimum değeri 18 aydır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="8ffc9-207">Ücretsiz iş koleksiyonlarındaki işleri 1 saat şeklinde minimum yapılandırabilir değere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="8ffc9-208">ISO 8601 biçiminde tanımlıdır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="8ffc9-209">Benzer şekilde, yeniden deneme sayısı değeri **retryCount** nesnesiyle belirtilir; bu yeniden denemeye çalışılacak sayıdır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="8ffc9-210">Varsayılan değer 4'tür ve maksimum değeri 20\ olduğu.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="8ffc9-211">Her ikisi de **Retryınterval** ve **retryCount** isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="8ffc9-212">**retryType** **sabit** olara ayarlanır ve açık şekilde bir değer belirtilmezse, bunlar belirtilen varsayılan değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="8ffc9-213">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8ffc9-213">See also</span></span>
 [<span data-ttu-id="8ffc9-214">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="8ffc9-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="8ffc9-215">Azure portalında Scheduler’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8ffc9-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="8ffc9-216">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="8ffc9-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="8ffc9-217">Azure Scheduler ile karmaşık zamanlamalar ve gelişmiş yineleme oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ffc9-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="8ffc9-218">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="8ffc9-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="8ffc9-219">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="8ffc9-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="8ffc9-220">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="8ffc9-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="8ffc9-221">Azure Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8ffc9-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="8ffc9-222">Azure Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8ffc9-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

