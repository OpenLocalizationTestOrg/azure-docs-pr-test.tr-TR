---
title: "Azure IOT Hub işleri anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - birden çok cihaz üzerinde çalışmasına işlerini zamanlama IOT hub'ına bağlı. İşler, etiketler ve istenen özelliklerini güncelleştirmek ve birden çok aygıta doğrudan yöntemleri çağırma."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="6e8d4-104">Birden fazla cihazda işleri zamanlama</span><span class="sxs-lookup"><span data-stu-id="6e8d4-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="6e8d4-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6e8d4-105">Overview</span></span>
<span data-ttu-id="6e8d4-106">Önceki makaleleri tarafından açıklandığı gibi Azure IOT hub'ı birkaç yapı taşlarını sağlar ([cihaz çifti özellikleri ve etiketleri] [ lnk-twin-devguide] ve [doğrudan yöntemleri][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="6e8d4-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="6e8d4-107">Genellikle, arka uç uygulamaları cihaz yöneticileri ve işleçleri güncelleştirmek ve IOT cihazları toplu ve zamanlanan saatte etkileşim etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="6e8d4-108">İşlerini cihaz çifti güncelleştirmeler ve bir cihaz kümesi karşı doğrudan yöntemleri yürütme zamanlama zaman kapsüller.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="6e8d4-109">Örneğin, bir işleç başlatmak ve bir grup oluşturma işlemlerini kesintiye uğratan olmayacaktır zaman 43 ve 3 kat oluşturmanın cihazı yeniden başlatmak için bir iş izleyen bir arka uç uygulaması kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="6e8d4-110">Kullanılması gereken durumlar</span><span class="sxs-lookup"><span data-stu-id="6e8d4-110">When to use</span></span>
<span data-ttu-id="6e8d4-111">Göz önünde bulundurun kullanarak, işlerin ne zaman: bir çözüm arka uç gereksinimlerini zamanlamak ve ilerleme durumunu izlemek için herhangi bir cihaz kümesi üzerinde şu etkinlikler:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="6e8d4-112">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="6e8d4-112">Update desired properties</span></span>
* <span data-ttu-id="6e8d4-113">Güncelleştirme etiketleri</span><span class="sxs-lookup"><span data-stu-id="6e8d4-113">Update tags</span></span>
* <span data-ttu-id="6e8d4-114">Doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="6e8d4-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="6e8d4-115">İş yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="6e8d4-115">Job lifecycle</span></span>
<span data-ttu-id="6e8d4-116">İşlerini çözüm arka ucu tarafından başlatılan ve IOT Hub tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="6e8d4-117">Bir hizmet dönük URI ile bir işi başlatabilirsiniz (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) ve bir hizmet dönük URI aracılığıyla yürütülen bir işin ilerleme için sorgu (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="6e8d4-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="6e8d4-118">Bir iş başlatıldıktan sonra işleri sorgulama işlerin durumunu yenilemek arka uç uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="6e8d4-119">Bir işi başlattığınızda özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir herhangi aşağıdaki kümesindeki dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="6e8d4-120">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-120">Reference topics:</span></span>
<span data-ttu-id="6e8d4-121">Aşağıdaki başvuru konuları işleri kullanma hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="6e8d4-122">İşlerini doğrudan bir yöntem yürütülemez</span><span class="sxs-lookup"><span data-stu-id="6e8d4-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="6e8d4-123">Yürütme için HTTP 1.1 istek ayrıntıları verilmiştir bir [doğrudan yöntemi] [ lnk-dev-methods] bir işi kullanarak cihazları bir dizi:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="6e8d4-124">Sorgu koşulu da tek bir cihaz kimliği veya aygıt aşağıda gösterildiği gibi kimlikleri listesini olabilir</span><span class="sxs-lookup"><span data-stu-id="6e8d4-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="6e8d4-125">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="6e8d4-126">[IOT Hub sorgu dili] [ lnk-query] IOT hub'ı sorgu dili ek ayrıntılı kapsar.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="6e8d4-127">Cihaz çifti özelliklerini güncelleştirmek için işlemler</span><span class="sxs-lookup"><span data-stu-id="6e8d4-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="6e8d4-128">Bir iş kullanarak cihaz çifti özelliklerini güncelleştirmek için HTTP 1.1 istek ayrıntıları verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="6e8d4-129">İşlerini ilerleme sorgulama</span><span class="sxs-lookup"><span data-stu-id="6e8d4-129">Querying for progress on jobs</span></span>
<span data-ttu-id="6e8d4-130">HTTP 1.1 istek ayrıntıları verilmiştir [işleri sorgulama][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="6e8d4-131">ContinuationToken yanıttan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="6e8d4-132">İşlerini özellikleri</span><span class="sxs-lookup"><span data-stu-id="6e8d4-132">Jobs Properties</span></span>
<span data-ttu-id="6e8d4-133">Özellikler ve sorgulanırken işleri veya iş sonuçları için kullanılabilir karşılık gelen açıklamaları listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="6e8d4-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="6e8d4-134">Property</span></span> | <span data-ttu-id="6e8d4-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6e8d4-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e8d4-136">**iş kimliği**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-136">**jobId**</span></span> |<span data-ttu-id="6e8d4-137">Uygulama Kimliği iş için sağlanan.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="6e8d4-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-138">**startTime**</span></span> |<span data-ttu-id="6e8d4-139">Uygulama için iş başlangıç zamanı (ISO 8601) sağlanan.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="6e8d4-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-140">**endTime**</span></span> |<span data-ttu-id="6e8d4-141">IOT hub'ı zaman iş tamamlandı (ISO 8601) tarihi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="6e8d4-142">Yalnızca iş 'Tamamlandı' durumuna ulaştıktan sonra geçerli.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="6e8d4-143">**türü**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-143">**type**</span></span> |<span data-ttu-id="6e8d4-144">İşlerini türleri:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-144">Types of jobs:</span></span> |
| <span data-ttu-id="6e8d4-145">**scheduledUpdateTwin**: İstenen özellikleri veya etiketleri kümesi güncelleştirmek için kullanılan bir işi.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="6e8d4-146">**scheduledDeviceMethod**: cihaz çiftlerini kümesi üzerinde bir aygıt yöntemi çağırmak için kullanılan bir işi.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="6e8d4-147">**durumu**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-147">**status**</span></span> |<span data-ttu-id="6e8d4-148">İşin geçerli durumu.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-148">Current state of the job.</span></span> <span data-ttu-id="6e8d4-149">Durum için olası değerler:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-149">Possible values for status:</span></span> |
| <span data-ttu-id="6e8d4-150">**Bekleyen** : Zamanlanmış ve iş hizmeti tarafından çekilmesi bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="6e8d4-151">**Zamanlanmış** : gelecekteki bir zamanı için zamanlanan.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="6e8d4-152">**çalışan** : şu anda etkin iş.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="6e8d4-153">**İptal** : işi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="6e8d4-154">**başarısız** : işi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="6e8d4-155">**Tamamlanan** : işi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="6e8d4-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="6e8d4-157">İş yürütme hakkındaki istatistiklerdir.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="6e8d4-158">**deviceJobStatistics** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="6e8d4-159">Özellik</span><span class="sxs-lookup"><span data-stu-id="6e8d4-159">Property</span></span> | <span data-ttu-id="6e8d4-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6e8d4-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e8d4-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="6e8d4-162">İşte cihaz sayısı.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="6e8d4-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="6e8d4-164">İş başarısız olduğu cihazlar sayısı.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="6e8d4-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="6e8d4-166">İş yeri başarılı cihaz sayısı.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="6e8d4-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="6e8d4-168">İşi çalışmakta olan aygıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="6e8d4-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="6e8d4-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="6e8d4-170">İşi çalıştırmak için beklemede olan aygıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="6e8d4-171">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="6e8d4-171">Additional reference material</span></span>
<span data-ttu-id="6e8d4-172">IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="6e8d4-173">[IOT Hub uç noktaları] [ lnk-endpoints] her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunan çeşitli uç noktaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="6e8d4-174">[Azaltma ve kotaları] [ lnk-quotas] IOT Hub hizmeti ve azaltma davranışı hizmetini kullandığınızda beklediğiniz uygulama kotaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="6e8d4-175">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] çeşitli dil SDK'ları listeler, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanın.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="6e8d4-176">[IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] IOT Hub'ından, cihaz çiftlerini ve işleri hakkında bilgi almak için kullanabileceğiniz IOT hub'ı sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="6e8d4-177">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] IOT hub'ı desteği hakkında daha fazla bilgi için MQTT Protokolü sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e8d4-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e8d4-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6e8d4-178">Next steps</span></span>
<span data-ttu-id="6e8d4-179">Bu makalede açıklanan kavramları bazıları denemek istiyorsanız, aşağıdaki IOT hub'ı öğreticide ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="6e8d4-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="6e8d4-180">[Zamanlama ve yayın işleri][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="6e8d4-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
