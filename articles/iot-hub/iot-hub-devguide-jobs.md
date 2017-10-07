---
title: "aaaUnderstand Azure IOT Hub işleri | Microsoft Docs"
description: "Geliştirici Kılavuzu - birden çok aygıta işleri toorun zamanlama tooyour IOT hub'ı bağlı. İşler, etiketler ve istenen özelliklerini güncelleştirmek ve birden çok aygıta doğrudan yöntemleri çağırma."
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="4708f-104">Birden fazla cihazda işleri zamanlama</span><span class="sxs-lookup"><span data-stu-id="4708f-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="4708f-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4708f-105">Overview</span></span>
<span data-ttu-id="4708f-106">Önceki makaleleri tarafından açıklandığı gibi Azure IOT hub'ı birkaç yapı taşlarını sağlar ([cihaz çifti özellikleri ve etiketleri] [ lnk-twin-devguide] ve [doğrudan yöntemleri][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="4708f-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="4708f-107">Genellikle, arka uç uygulamalar aygıt Yöneticiler ve İşletmenleri tooupdate etkinleştirin ve IOT cihazları toplu ve zamanlanan saatte etkileşim.</span><span class="sxs-lookup"><span data-stu-id="4708f-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="4708f-108">İşlerini zamanlama zaman hello yürütme cihaz çifti güncelleştirmeleri ve bir cihaz kümesi karşı doğrudan yöntemlerin kapsüller.</span><span class="sxs-lookup"><span data-stu-id="4708f-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="4708f-109">Örneğin, bir işleç başlatmak ve iş tooreboot 43 ve 3 kat hello oluşturma işlemlerini kesintiye uğratan toohello olmayacaktır aynı anda oluşturmanın cihazlar izleyen bir arka uç uygulaması kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="4708f-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="4708f-110">Zaman toouse</span><span class="sxs-lookup"><span data-stu-id="4708f-110">When toouse</span></span>
<span data-ttu-id="4708f-111">Göz önünde bulundurun kullanarak, işlerin ne zaman: bir çözüm arka ucu gereksinimlerini tooschedule ve izleme herhangi bir cihaz kümesine etkinlikleri izleyerek hello ilerleme:</span><span class="sxs-lookup"><span data-stu-id="4708f-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="4708f-112">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="4708f-112">Update desired properties</span></span>
* <span data-ttu-id="4708f-113">Güncelleştirme etiketleri</span><span class="sxs-lookup"><span data-stu-id="4708f-113">Update tags</span></span>
* <span data-ttu-id="4708f-114">Doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="4708f-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="4708f-115">İş yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="4708f-115">Job lifecycle</span></span>
<span data-ttu-id="4708f-116">İşlerini hello çözüm arka ucu tarafından başlatılan ve IOT Hub tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="4708f-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="4708f-117">Bir hizmet dönük URI ile bir işi başlatabilirsiniz (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) ve bir hizmet dönük URI aracılığıyla yürütülen bir işin ilerleme için sorgu (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="4708f-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="4708f-118">Bir iş başlatıldıktan sonra işleri sorgulama çalışan işi hello arka uç uygulama toorefresh hello durumu sağlar.</span><span class="sxs-lookup"><span data-stu-id="4708f-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="4708f-119">Bir işi başlattığınızda özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir kümesi aşağıdaki hello birinde dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="4708f-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="4708f-120">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="4708f-120">Reference topics:</span></span>
<span data-ttu-id="4708f-121">başvuru konuları aşağıdaki hello işleri kullanma hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4708f-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="4708f-122">İşlerini tooexecute doğrudan yöntemleri</span><span class="sxs-lookup"><span data-stu-id="4708f-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="4708f-123">Merhaba yürütmek hello HTTP 1.1 İstek Ayrıntıları aşağıdadır bir [doğrudan yöntemi] [ lnk-dev-methods] bir işi kullanarak cihazları bir dizi:</span><span class="sxs-lookup"><span data-stu-id="4708f-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="4708f-124">Merhaba sorgu koşulu da tek bir cihaz kimliği veya aygıt kimliklerinin bir listesi aşağıda gösterildiği gibi olabilir</span><span class="sxs-lookup"><span data-stu-id="4708f-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="4708f-125">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="4708f-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="4708f-126">[IOT Hub sorgu dili] [ lnk-query] IOT hub'ı sorgu dili ek ayrıntılı kapsar.</span><span class="sxs-lookup"><span data-stu-id="4708f-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="4708f-127">İşlerini tooupdate cihaz çifti özellikleri</span><span class="sxs-lookup"><span data-stu-id="4708f-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="4708f-128">Merhaba, bir iş kullanarak cihaz çifti özelliklerini güncelleştirmek için HTTP 1.1 hello İstek Ayrıntıları aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="4708f-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="4708f-129">İşlerini ilerleme sorgulama</span><span class="sxs-lookup"><span data-stu-id="4708f-129">Querying for progress on jobs</span></span>
<span data-ttu-id="4708f-130">Merhaba hello için HTTP 1.1 İstek Ayrıntıları aşağıdadır [işleri sorgulama][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="4708f-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="4708f-131">Merhaba continuationToken hello yanıttan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="4708f-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="4708f-132">İşlerini özellikleri</span><span class="sxs-lookup"><span data-stu-id="4708f-132">Jobs Properties</span></span>
<span data-ttu-id="4708f-133">Merhaba, özellikleri ve sorgulanırken işleri veya iş sonuçları için kullanılabilir karşılık gelen açıklamaları listesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="4708f-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="4708f-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="4708f-134">Property</span></span> | <span data-ttu-id="4708f-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4708f-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4708f-136">**iş kimliği**</span><span class="sxs-lookup"><span data-stu-id="4708f-136">**jobId**</span></span> |<span data-ttu-id="4708f-137">Uygulama Kimliği hello işi için sağlanan.</span><span class="sxs-lookup"><span data-stu-id="4708f-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="4708f-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="4708f-138">**startTime**</span></span> |<span data-ttu-id="4708f-139">Merhaba işi için sağlanan uygulama başlangıç saati (ISO 8601).</span><span class="sxs-lookup"><span data-stu-id="4708f-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="4708f-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="4708f-140">**endTime**</span></span> |<span data-ttu-id="4708f-141">Merhaba işi tamamlandığında IOT hub'ı tarih (ISO 8601) için sağlanan.</span><span class="sxs-lookup"><span data-stu-id="4708f-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="4708f-142">Yalnızca 'Tamamlandı' hello durumu hello iş ulaştıktan sonra geçerli.</span><span class="sxs-lookup"><span data-stu-id="4708f-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="4708f-143">**türü**</span><span class="sxs-lookup"><span data-stu-id="4708f-143">**type**</span></span> |<span data-ttu-id="4708f-144">İşlerini türleri:</span><span class="sxs-lookup"><span data-stu-id="4708f-144">Types of jobs:</span></span> |
| <span data-ttu-id="4708f-145">**scheduledUpdateTwin**: kullanılan iş tooupdate istenen özellikleri veya etiketleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="4708f-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="4708f-146">**scheduledDeviceMethod**: kullanılan iş tooinvoke bir dizi cihaz çiftlerini cihaz yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4708f-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="4708f-147">**durumu**</span><span class="sxs-lookup"><span data-stu-id="4708f-147">**status**</span></span> |<span data-ttu-id="4708f-148">Merhaba işin geçerli durumu.</span><span class="sxs-lookup"><span data-stu-id="4708f-148">Current state of hello job.</span></span> <span data-ttu-id="4708f-149">Durum için olası değerler:</span><span class="sxs-lookup"><span data-stu-id="4708f-149">Possible values for status:</span></span> |
| <span data-ttu-id="4708f-150">**Bekleyen** : Zamanlanmış ve bekleme toobe hello iş hizmeti tarafından toplanma.</span><span class="sxs-lookup"><span data-stu-id="4708f-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="4708f-151">**Zamanlanmış** : hello gelecekteki bir süre için zamanlanan.</span><span class="sxs-lookup"><span data-stu-id="4708f-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="4708f-152">**çalışan** : şu anda etkin iş.</span><span class="sxs-lookup"><span data-stu-id="4708f-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="4708f-153">**İptal** : işi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="4708f-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="4708f-154">**başarısız** : işi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="4708f-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="4708f-155">**Tamamlanan** : işi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="4708f-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="4708f-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="4708f-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="4708f-157">Merhaba işin yürütme hakkındaki istatistiklerdir.</span><span class="sxs-lookup"><span data-stu-id="4708f-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="4708f-158">**deviceJobStatistics** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="4708f-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="4708f-159">Özellik</span><span class="sxs-lookup"><span data-stu-id="4708f-159">Property</span></span> | <span data-ttu-id="4708f-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4708f-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4708f-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="4708f-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="4708f-162">Cihazların Merhaba işi sayısı.</span><span class="sxs-lookup"><span data-stu-id="4708f-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="4708f-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="4708f-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="4708f-164">Merhaba iş başarısız olduğu cihazlar sayısı.</span><span class="sxs-lookup"><span data-stu-id="4708f-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="4708f-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="4708f-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="4708f-166">Burada hello iş başarılı cihaz sayısı.</span><span class="sxs-lookup"><span data-stu-id="4708f-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="4708f-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="4708f-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="4708f-168">Merhaba işi çalışmakta olan aygıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="4708f-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="4708f-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="4708f-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="4708f-170">Toorun hello işi olan aygıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="4708f-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="4708f-171">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="4708f-171">Additional reference material</span></span>
<span data-ttu-id="4708f-172">Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="4708f-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4708f-173">[IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.</span><span class="sxs-lookup"><span data-stu-id="4708f-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="4708f-174">[Azaltma ve kotaları] [ lnk-quotas] toohello IOT Hub hizmetine uygulamak ve hello hizmetini kullandığınızda azaltma davranışı tooexpect hello hello kotaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="4708f-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="4708f-175">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanın.</span><span class="sxs-lookup"><span data-stu-id="4708f-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="4708f-176">[IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] hello tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz IOT hub'ı sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="4708f-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="4708f-177">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4708f-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4708f-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4708f-178">Next steps</span></span>
<span data-ttu-id="4708f-179">Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticiyi izleyerek hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="4708f-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="4708f-180">[Zamanlama ve yayın işleri][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4708f-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
