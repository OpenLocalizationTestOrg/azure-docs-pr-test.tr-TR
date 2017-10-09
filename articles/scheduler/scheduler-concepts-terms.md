---
title: "aaaScheduler kavramları, terimleri ve varlıkları | Microsoft Docs"
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
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="fceb9-104">Scheduler kavramları ve terminolojisi + varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="fceb9-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="fceb9-105">Scheduler varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="fceb9-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="fceb9-106">Merhaba aşağıdaki tabloda gösterilen ya da hello Scheduler API'si tarafından kullanılan hello ana kaynaklar açıklanır:</span><span class="sxs-lookup"><span data-stu-id="fceb9-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="fceb9-107">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fceb9-107">Resource</span></span> | <span data-ttu-id="fceb9-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fceb9-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fceb9-109">**İş koleksiyonu**</span><span class="sxs-lookup"><span data-stu-id="fceb9-109">**Job collection**</span></span> |<span data-ttu-id="fceb9-110">İş koleksiyonu, bir grup işi içerir ve ayarlar, kotalar ve hello koleksiyondaki işler tarafından paylaşılan kısıtlamaları tutar.</span><span class="sxs-lookup"><span data-stu-id="fceb9-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="fceb9-111">İş koleksiyonu abonelik sahibi tarafından oluşturulur ve işleri kullanım veya uygulama sınırlarına göre gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="fceb9-112">Kısıtlanmış tooone bölgedir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-112">It’s constrained tooone region.</span></span> <span data-ttu-id="fceb9-113">Ayrıca hello zorlama kotaları koleksiyonda tooconstrain hello tüm işlerin kullanımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fceb9-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="fceb9-114">Merhaba kotalar MaxJobs ve maxrecurrence değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="fceb9-115">**İş**</span><span class="sxs-lookup"><span data-stu-id="fceb9-115">**Job**</span></span> |<span data-ttu-id="fceb9-116">Bir iş, yürütmek üzere basit ya da karmaşık stratejilerle tek bir yinelenen eylemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fceb9-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="fceb9-117">Eylemler HTTP, depolama kuyruğu, hizmet veri yolu kuyruğu ya da hizmet veri yolu konusu isteklerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="fceb9-118">**İş geçmişi**</span><span class="sxs-lookup"><span data-stu-id="fceb9-118">**Job history**</span></span> |<span data-ttu-id="fceb9-119">İş geçmişi bir işin yürütülmesine ilişkin ayrıntılarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fceb9-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="fceb9-120">Bu başarılı ve hatalı karşılaştırmasının yanı sıra tüm yanıt ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="fceb9-121">Scheduler varlık yönetimi</span><span class="sxs-lookup"><span data-stu-id="fceb9-121">Scheduler entity management</span></span>
<span data-ttu-id="fceb9-122">Yüksek bir düzeyde hello kaynaklar üzerinde işlem aşağıdaki hello hello Zamanlayıcı ve hello Hizmet Yönetimi API'si ortaya çıkarır:</span><span class="sxs-lookup"><span data-stu-id="fceb9-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="fceb9-123">Özellik</span><span class="sxs-lookup"><span data-stu-id="fceb9-123">Capability</span></span> | <span data-ttu-id="fceb9-124">Açıklama ve URI adresi</span><span class="sxs-lookup"><span data-stu-id="fceb9-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="fceb9-125">**İş koleksiyonu yönetimi**</span><span class="sxs-lookup"><span data-stu-id="fceb9-125">**Job collection management**</span></span> |<span data-ttu-id="fceb9-126">Al koy ve Sil desteği oluşturma ve iş koleksiyonları ve burada yer alan hello işleri değiştirme.</span><span class="sxs-lookup"><span data-stu-id="fceb9-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="fceb9-127">İş koleksiyonu işleri için bir kapsayıcıdır ve tooquotas ve paylaşılan ayarları eşler.</span><span class="sxs-lookup"><span data-stu-id="fceb9-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="fceb9-128">İleride açıklanan kota örnekleri, maksimum iş sayısı ve en küçük yineleme aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="fceb9-129">KOY ve SİL: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="fceb9-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="fceb9-130">AL: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="fceb9-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="fceb9-131">**İş yönetimi**</span><span class="sxs-lookup"><span data-stu-id="fceb9-131">**Job management**</span></span> |<span data-ttu-id="fceb9-132">İşleri oluşturma ve değiştirmeye yönelik AL, KOY, YAYIMLA, DÜZELTME EKİ UYGULA ve SİL desteği.</span><span class="sxs-lookup"><span data-stu-id="fceb9-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="fceb9-133">Açık oluşturma böylece tüm işleri zaten var, tooa iş koleksiyonu ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="fceb9-134">**İş geçmişi yönetimi**</span><span class="sxs-lookup"><span data-stu-id="fceb9-134">**Job history management**</span></span> |<span data-ttu-id="fceb9-135">İş geçen süresi ve iş yürütme sonuçları gibi, 60 günlük iş yürütme geçmişi getirmek üzere AL desteği.</span><span class="sxs-lookup"><span data-stu-id="fceb9-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="fceb9-136">Durum ve duruma göre filtreleme için sorgu dizesi parametresi desteği ekler.</span><span class="sxs-lookup"><span data-stu-id="fceb9-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="fceb9-137">İş türleri</span><span class="sxs-lookup"><span data-stu-id="fceb9-137">Job types</span></span>
<span data-ttu-id="fceb9-138">Birden çok iş türü vardır: HTTP işleri (SSL destekleyen HTTPS işleri dahil), depolama kuyruğu işleri, hizmet veri yolu kuyruğu işleri ve hizmet veri yolu konusu işleri.</span><span class="sxs-lookup"><span data-stu-id="fceb9-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="fceb9-139">HTTP işleri, mevcut bir iş yükünde ya da hizmette uç noktaya sahipseniz idealdir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="fceb9-140">Bu işleri depolama kuyrukları kullanan iş yükleri için ideal; bu nedenle depolama kuyruğu işleri toopost iletileri toostorage kuyrukları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fceb9-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="fceb9-141">Benzer şekilde, hizmet veri yolu işleri hizmet veri yolu kuyrukları ve konuları kullanan iş yükleri için idealdir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="fceb9-142">Merhaba ayrıntılı "job" varlığı</span><span class="sxs-lookup"><span data-stu-id="fceb9-142">hello "job" entity in detail</span></span>
<span data-ttu-id="fceb9-143">Temel düzeyde, zamanlanan bir iş birkaç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="fceb9-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="fceb9-144">Merhaba iş Zamanlayıcı başlatıldığında hello eylem tooperform</span><span class="sxs-lookup"><span data-stu-id="fceb9-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="fceb9-145">(İsteğe bağlı) hello süresi toorun hello işi</span><span class="sxs-lookup"><span data-stu-id="fceb9-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="fceb9-146">(İsteğe bağlı) Zaman ve ne sıklıkta toorepeat hello işi</span><span class="sxs-lookup"><span data-stu-id="fceb9-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="fceb9-147">(İsteğe bağlı) Merhaba birincil eylem başarısız olursa eylem toofire</span><span class="sxs-lookup"><span data-stu-id="fceb9-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="fceb9-148">Dahili olarak, zamanlanmış bir işi hello sonraki zamanlanan yürütme zamanı gibi sistem tarafından sağlanan verileri de içerir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="fceb9-149">koddan hello zamanlanan bir işin kapsamlı bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="fceb9-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="fceb9-150">Ayrıntılar sonraki bölümlerde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-150">Details are provided in subsequent sections.</span></span>

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
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
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

<span data-ttu-id="fceb9-151">Merhaba örnek zamanlanan İşte yukarıdaki görüldüğü gibi bir iş tanımı birkaç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="fceb9-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="fceb9-152">Başlangıç zamanı ("startTime")</span><span class="sxs-lookup"><span data-stu-id="fceb9-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="fceb9-153">Hata eylemi ("errorAction") içeren eylem ("eylem")</span><span class="sxs-lookup"><span data-stu-id="fceb9-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="fceb9-154">Yineleme ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="fceb9-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="fceb9-155">Durum ("state")</span><span class="sxs-lookup"><span data-stu-id="fceb9-155">State (“state”)</span></span>  
* <span data-ttu-id="fceb9-156">Durum ("status")</span><span class="sxs-lookup"><span data-stu-id="fceb9-156">Status (“status”)</span></span>  
* <span data-ttu-id="fceb9-157">Yeniden deneme ilkesi ("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="fceb9-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="fceb9-158">Şimdi bunların her birini ayrıntılı inceleyelim:</span><span class="sxs-lookup"><span data-stu-id="fceb9-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="fceb9-159">startTime</span><span class="sxs-lookup"><span data-stu-id="fceb9-159">startTime</span></span>
<span data-ttu-id="fceb9-160">Merhaba "startTime" Merhaba başlangıç saati ve hello arayan toospecify hello hat üzerinde uzaklığı bir saat dilimi sağlar [ISO 8601 biçiminde](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="fceb9-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="fceb9-161">action ve errorAction</span><span class="sxs-lookup"><span data-stu-id="fceb9-161">action and errorAction</span></span>
<span data-ttu-id="fceb9-162">Merhaba "action" her meydana Gelişte çağrılan hello eylemdir ve hizmet başlatma türünü açıklar.</span><span class="sxs-lookup"><span data-stu-id="fceb9-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="fceb9-163">Merhaba zamanlama sağlanan hello üzerinde yürütülecek eylemdir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="fceb9-164">Scheduler, HTTP, depolama kuyruğu, hizmet veri yolu konusu ve hizmet veri yolu kuyruğu eylemlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="fceb9-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="fceb9-165">Yukarıdaki hello örnekte Hello eylem bir HTTP eylemdir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="fceb9-166">Bir depolama kuyruğu eylemi örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fceb9-166">Below is an example of a storage queue action:</span></span>

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

<span data-ttu-id="fceb9-167">Bir hizmet veri yolu konusu eylemi örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fceb9-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="fceb9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="fceb9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="fceb9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="fceb9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="fceb9-170">Bir hizmet veri yolu kuyruğu eylemi örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fceb9-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="fceb9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="fceb9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="fceb9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // netMessaging ya da AMQP olabilir "authentication": {</span><span class="sxs-lookup"><span data-stu-id="fceb9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="fceb9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="fceb9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="fceb9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="fceb9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="fceb9-175">Merhaba "errorAction" Merhaba hata hello eylemin hello birincil eylem başarısız olduğunda çağrılan işleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="fceb9-176">Bu değişken toocall bir hata işleme uç nokta kullanın veya bir kullanıcı bildirimi gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fceb9-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="fceb9-177">Bu kullanılabilir o hello hello durumda ikincil uç noktaya ulaşmak için birincil kullanılabilir (örneğin, bir olağanüstü durum hello uç noktanın sitede durumunu hello) değil veya bir hata işleme uç noktasını bildirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="fceb9-178">Yalnızca hello birincil eylemde olduğu gibi hello hata eylemi diğer eylemler temelinde basit ya da birleşik mantıklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="fceb9-179">toocreate bir SAS belirteci başvurmak çok nasıl toolearn[oluşturmak ve paylaşılan erişim imzası kullanmak](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="fceb9-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="fceb9-180">yineleme</span><span class="sxs-lookup"><span data-stu-id="fceb9-180">recurrence</span></span>
<span data-ttu-id="fceb9-181">Yineleme birkaç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="fceb9-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="fceb9-182">Sıklık: Dakika, saat, gün, hafta, ay, yıldan biri</span><span class="sxs-lookup"><span data-stu-id="fceb9-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="fceb9-183">Aralığı: Merhaba yinelemesi sıklığı verilen hello aralıkta</span><span class="sxs-lookup"><span data-stu-id="fceb9-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="fceb9-184">Belirtilen zamanlama: dakika, saat, hafta, ay ve ayın günü hello yinelenme belirtin</span><span class="sxs-lookup"><span data-stu-id="fceb9-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="fceb9-185">Sayı: Yineleme sayısı</span><span class="sxs-lookup"><span data-stu-id="fceb9-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="fceb9-186">Bitiş saati: hello belirtilen bitiş zamanından sonra hiç iş yürütülmez</span><span class="sxs-lookup"><span data-stu-id="fceb9-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="fceb9-187">Bir iş, JSON tanımında belirtilen yinelenen nesneye sahipse yinelenendir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="fceb9-188">Sayı ve endTime belirtilmişse, önce gerçekleşirse hello tamamlama kuralı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="fceb9-189">durum</span><span class="sxs-lookup"><span data-stu-id="fceb9-189">state</span></span>
<span data-ttu-id="fceb9-190">hello iş Hello durumu dört değerden biridir: etkin, devre dışı, tamamlandı ya da hatalı.</span><span class="sxs-lookup"><span data-stu-id="fceb9-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="fceb9-191">KOYABİLİRSİNİZ veya düzeltme eki işler bunu tooupdate bunları toohello etkin veya devre dışı durumu.</span><span class="sxs-lookup"><span data-stu-id="fceb9-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="fceb9-192">Bir işi tamamlandı ya da hatalı ise (Merhaba iş hala silinebilir) güncelleştirilemiyor son durum olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="fceb9-193">Merhaba state özelliği örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fceb9-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="fceb9-194">Tamamlanan ve hatalı işler 60 gün sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="fceb9-195">durum</span><span class="sxs-lookup"><span data-stu-id="fceb9-195">status</span></span>
<span data-ttu-id="fceb9-196">Scheduler işi başladıktan sonra hello geçerli hello işin durumu hakkında bilgi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="fceb9-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="fceb9-197">Bu nesne hello kullanıcı tarafından ayarlanamaz değildir — hello sistem tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="fceb9-198">Ancak, böylece bir hello işin durumunu kolayca edinebileceği hello iş nesnesi (yerine ayrı bağlantılı bir kaynak) dahil.</span><span class="sxs-lookup"><span data-stu-id="fceb9-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="fceb9-199">İş durumu içerir hello önceki yürütme (varsa), başlangıç zamanı hello hello sonraki zamanlanan yürütmeyi (devam eden işler) süresi ve hello iş hello yürütme sayısı.</span><span class="sxs-lookup"><span data-stu-id="fceb9-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="fceb9-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="fceb9-200">retryPolicy</span></span>
<span data-ttu-id="fceb9-201">Scheduler işi başarısız olursa, olası toospecify olup olmadığını ve nasıl hello eylemin yeniden denenip bir yeniden deneme ilkesi toodetermine olur.</span><span class="sxs-lookup"><span data-stu-id="fceb9-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="fceb9-202">Bu hello tarafından belirlenir **retryType** nesne — çok ayarlamak**hiçbiri** varsa yeniden deneme ilkesi, yukarıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="fceb9-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="fceb9-203">Çok ayarlamak**sabit** bir yeniden deneme ilkesi varsa.</span><span class="sxs-lookup"><span data-stu-id="fceb9-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="fceb9-204">tooset bir yeniden deneme ilkesi iki ek ayar belirtilebilir: yeniden deneme aralığını (**Retryınterval**) ve yeniden deneme sayısı hello (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="fceb9-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="fceb9-205">Merhaba, Hello ile belirtilen yeniden deneme aralığı **Retryınterval** nesne, hello yeniden denemeler arasındaki aralıktır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="fceb9-206">Varsayılan değer 30 saniye, minimum yapılandırılabilir değeri 15 saniye, ve maksimum değeri 18 aydır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="fceb9-207">Ücretsiz iş koleksiyonlarındaki işleri 1 saat şeklinde minimum yapılandırabilir değere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fceb9-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="fceb9-208">Merhaba ISO 8601 biçiminde tanımlıdır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="fceb9-209">Yeniden deneme sayısı hello hello değerini hello ile benzer şekilde, belirtilen **retryCount** nesne; hello kaç kez yeniden değil.</span><span class="sxs-lookup"><span data-stu-id="fceb9-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="fceb9-210">Varsayılan değer 4'tür ve maksimum değeri 20\ olduğu.</span><span class="sxs-lookup"><span data-stu-id="fceb9-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="fceb9-211">Her ikisi de **Retryınterval** ve **retryCount** isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fceb9-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="fceb9-212">Bunlar varsayılan değerlerine verilir **retryType** çok ayarlanır**sabit** ve açıkça değer belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="fceb9-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="fceb9-213">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="fceb9-213">See also</span></span>
 [<span data-ttu-id="fceb9-214">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="fceb9-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="fceb9-215">Zamanlayıcı hello Azure portalını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fceb9-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="fceb9-216">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="fceb9-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="fceb9-217">Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile</span><span class="sxs-lookup"><span data-stu-id="fceb9-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="fceb9-218">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="fceb9-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="fceb9-219">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="fceb9-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="fceb9-220">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="fceb9-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="fceb9-221">Azure Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="fceb9-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="fceb9-222">Azure Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fceb9-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

