---
title: Azure IOT Hub sorgu dili anlama | Microsoft Docs
description: "Geliştirici Kılavuzu - IOT hub'dan cihaz çiftlerini ve işleri hakkında bilgi almak için kullanılan SQL benzeri IOT hub'ı sorgu dili açıklaması."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="e08b7-103">Başvuru - cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili</span><span class="sxs-lookup"><span data-stu-id="e08b7-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="e08b7-104">IOT hub'ı sağlayan bilgi almak için güçlü bir SQL benzeri dili ile ilgili [cihaz çiftlerini] [ lnk-twins] ve [işleri][lnk-jobs], ve [ileti yönlendirme][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="e08b7-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="e08b7-105">Bu makalede sunar:</span><span class="sxs-lookup"><span data-stu-id="e08b7-105">This article presents:</span></span>

* <span data-ttu-id="e08b7-106">Önemli özellikleri giriş IOT hub'ı sorgu dili ve</span><span class="sxs-lookup"><span data-stu-id="e08b7-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="e08b7-107">Dil ayrıntılı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="e08b7-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="e08b7-108">Cihaz çifti sorguları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e08b7-108">Get started with device twin queries</span></span>
<span data-ttu-id="e08b7-109">[Cihaz çiftlerini] [ lnk-twins] etiketleri ve özellikleri rastgele JSON nesnelerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="e08b7-110">IOT Hub, tüm cihaz çifti bilgilerini içeren tek bir JSON belgesi olarak sorgu cihaz çiftlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e08b7-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="e08b7-111">Örneğin, IOT hub cihaz çiftlerini aşağıdaki yapısını olduğunu varsayın:</span><span class="sxs-lookup"><span data-stu-id="e08b7-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="e08b7-112">IOT Hub cihaz çiftlerini adlı bir belge koleksiyonu olarak kullanıma sunar **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="e08b7-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="e08b7-113">Bu nedenle aşağıdaki sorgu tüm cihaz çiftlerini kümesini alır:</span><span class="sxs-lookup"><span data-stu-id="e08b7-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="e08b7-114">[Azure IOT SDK'ları] [ lnk-hub-sdks] büyük sonuçlarının disk belleği destekler.</span><span class="sxs-lookup"><span data-stu-id="e08b7-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="e08b7-115">IOT Hub cihaz çiftlerini rasgele koşullarla filtreleme almanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="e08b7-116">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="e08b7-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="e08b7-117">ile cihaz çiftlerini alır **location.region** etiketi kümesine **ABD**.</span><span class="sxs-lookup"><span data-stu-id="e08b7-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="e08b7-118">Boole işleçleri ve aritmetik karşılaştırmaları de, örneğin desteklenir</span><span class="sxs-lookup"><span data-stu-id="e08b7-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="e08b7-119">telemetri dakikada daha az sıklıkta göndermek için yapılandırılan ABD bulunan tüm cihaz çiftlerini alır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="e08b7-120">Bir kolaylık da dizi sabitleri ile kullanmak mümkündür **IN** ve **NBU** (içinde değil) işleçler.</span><span class="sxs-lookup"><span data-stu-id="e08b7-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="e08b7-121">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="e08b7-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="e08b7-122">WiFi bildirilen veya bağlantı kablolu tüm cihaz çiftlerini alır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="e08b7-123">Genellikle, belirli bir özellik içeren tüm cihaz çiftlerini tanımlamak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="e08b7-124">IOT hub'ı destekleyen işlevi `is_defined()` bu amaç için.</span><span class="sxs-lookup"><span data-stu-id="e08b7-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="e08b7-125">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="e08b7-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="e08b7-126">tanımladığınız tüm cihaz çiftlerini alınan `connectivity` özelliği bildirdi.</span><span class="sxs-lookup"><span data-stu-id="e08b7-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="e08b7-127">Başvurmak [WHERE yan tümcesi] [ lnk-query-where] filtreleme yetenekleri tam başvuru için bölüm.</span><span class="sxs-lookup"><span data-stu-id="e08b7-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="e08b7-128">Gruplandırma ve toplamalar da desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="e08b7-129">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="e08b7-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="e08b7-130">cihaz sayısı her telemetri yapılandırma durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-130">returns the count of the devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="e08b7-131">Önceki örnekte olduğu üç aygıt başarılı bir yapılandırma bildirilen, iki hala yapılandırmayı uygulama ve bir hata bildirdi bir durum gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="e08b7-132">C# örnek</span><span class="sxs-lookup"><span data-stu-id="e08b7-132">C# example</span></span>
<span data-ttu-id="e08b7-133">Sorgu işlevi tarafından sunulan [C# hizmeti SDK'sını] [ lnk-hub-sdks] içinde **RegistryManager** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e08b7-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="e08b7-134">Burada, basit bir sorgu örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="e08b7-135">Not nasıl **sorgu** nesne örneği içeren bir sayfa boyutunu (en fazla 1000) ve sonra birden çok sayfa çağırarak alınabilir **GetNextAsTwinAsync** yöntemleri birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="e08b7-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="e08b7-136">Sorgu nesnesi birden çok sunan Not **sonraki\***bağlı olarak cihaz çiftine veya iş nesneleri veya düz JSON gibi sorgu tarafından tahminleri kullanırken kullanılması gereken seri durumdan çıkarma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e08b7-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="e08b7-137">Node.js örneği</span><span class="sxs-lookup"><span data-stu-id="e08b7-137">Node.js example</span></span>
<span data-ttu-id="e08b7-138">Sorgu işlevi tarafından sunulan [Node.js için Azure IOT hizmeti SDK'sını] [ lnk-hub-sdks] içinde **kayıt defteri** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="e08b7-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="e08b7-139">Burada, basit bir sorgu örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="e08b7-140">Not nasıl **sorgu** nesne örneği içeren bir sayfa boyutunu (en fazla 1000) ve sonra birden çok sayfa çağırarak alınabilir **nextAsTwin** yöntemleri birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="e08b7-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="e08b7-141">Sorgu nesnesi birden çok sunan Not **sonraki\***bağlı olarak cihaz çiftine veya iş nesneleri veya düz JSON gibi sorgu tarafından tahminleri kullanırken kullanılması gereken seri durumdan çıkarma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e08b7-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="e08b7-142">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="e08b7-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e08b7-143">Sorgu sonuçları en son değerleri göre gecikme birkaç dakika içinde cihaz çiftlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="e08b7-144">Tek tek cihaz çiftlerini kimliğine göre sorgulama, her zaman, her zaman en son değerleri içerir ve daha yüksek azaltma sınırları almak cihaz çifti API kullanılması tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="e08b7-145">Şu anda karşılaştırmaları yalnızca ilkel türler arasında (hiçbir nesne), örneğin desteklenir `... WHERE properties.desired.config = properties.reported.config` yalnızca bu özellikleri ilkel değerler varsa desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="e08b7-146">İşlerini sorguları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e08b7-146">Get started with jobs queries</span></span>
<span data-ttu-id="e08b7-147">[İşlerini] [ lnk-jobs] aygıtların kümeleri üzerinde işlemlerini yürütmek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="e08b7-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="e08b7-148">Her cihaz çifti bilgilerin onu olduğu adlı bir koleksiyon bölümünde işlerin içeren **işleri**.</span><span class="sxs-lookup"><span data-stu-id="e08b7-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="e08b7-149">Mantıksal olarak</span><span class="sxs-lookup"><span data-stu-id="e08b7-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="e08b7-150">Bu koleksiyon şu anda olarak sorgulanabilir **devices.jobs** IOT hub'ı sorgu dili.</span><span class="sxs-lookup"><span data-stu-id="e08b7-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e08b7-151">İşlerini özelliği şu anda hiçbir zaman cihaz çiftlerini (diğer bir deyişle, 'aygıtlardan' içeren sorgular) sorgulanırken döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="e08b7-152">Yalnızca doğrudan sorgu kullanarak erişilebilir `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="e08b7-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="e08b7-153">Örneğin, tek bir cihazı etkileyen tüm işleri (Geçmiş ve zamanlanmış) almak için aşağıdaki sorguyu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e08b7-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="e08b7-154">Bu sorgu, cihaza özel durumu (ve büyük olasılıkla doğrudan yöntemi yanıtı) döndürülen her bir iş nasıl sağladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e08b7-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="e08b7-155">Tüm nesne özelliklerinde rastgele Boolean koşullara ile filtrelemek mümkündür **devices.jobs** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="e08b7-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="e08b7-156">Örneğin, aşağıdaki sorguyu:</span><span class="sxs-lookup"><span data-stu-id="e08b7-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="e08b7-157">Tüm tamamlanan alır cihaz çifti güncelleştirme işleri aygıtın **myDeviceId** Eylül 2016 sonra oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="e08b7-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="e08b7-158">Tek bir işin cihaz başına sonuçlar almak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="e08b7-159">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="e08b7-159">Limitations</span></span>
<span data-ttu-id="e08b7-160">Üzerinde şu anda sorgular **devices.jobs** desteklemez:</span><span class="sxs-lookup"><span data-stu-id="e08b7-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="e08b7-161">Projeksiyonlar, bu nedenle yalnızca `SELECT *` mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="e08b7-162">Proje Özellikleri (önceki bölüme bakın) ek olarak cihaz çiftine başvurmak koşulları.</span><span class="sxs-lookup"><span data-stu-id="e08b7-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="e08b7-163">Count, avg, grupla gibi toplamalar gerçekleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="e08b7-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="e08b7-164">Cihaz bulut ileti yollar sorgu ifadeleri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e08b7-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="e08b7-165">Kullanarak [cihaz bulut yolları][lnk-devguide-messaging-routes], IOT Hub'ın tek bir ileti karşı değerlendirilen ifadeleri göre farklı uç noktalar için cihaz bulut iletilerini gönderilmesi için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e08b7-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="e08b7-166">Rota [koşulu] [ lnk-query-expressions] twin ve iş sorguları koşullarında olarak aynı IOT hub'ı sorgu dilini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="e08b7-167">Rota koşullar ileti üstbilgilerini ve gövde üzerinde değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="e08b7-168">Yönlendirme sorgu ifadesi yalnızca ileti gövdesi, yalnızca ileti üstbilgilerini gerektirebilir veya her ikisi de üstbilgileri iletisi ve ileti gövdesi.</span><span class="sxs-lookup"><span data-stu-id="e08b7-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="e08b7-169">IOT hub'ı iletileri yönlendirmek için üstbilgiler ve ileti gövdesi için belirli bir şema varsayar ve aşağıdaki bölümlerde IOT Hub'ın düzgün bir şekilde yönlendirmek gereklidir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="e08b7-170">İleti üstbilgilerinde yönlendirme</span><span class="sxs-lookup"><span data-stu-id="e08b7-170">Routing on message headers</span></span>

<span data-ttu-id="e08b7-171">IOT Hub aşağıdaki JSON gösterimi ileti yönlendirme iletisi üstbilgilerinin varsayılır:</span><span class="sxs-lookup"><span data-stu-id="e08b7-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="e08b7-172">İleti sistemi özelliklerini öneki ile `'$'` simgesi.</span><span class="sxs-lookup"><span data-stu-id="e08b7-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="e08b7-173">Kullanıcı özellikleri her zaman kendi adıyla erişilir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="e08b7-174">Bir kullanıcı özellik adı bir sistem özelliği ile çakıştığı için ortaya çıkarsa (gibi `$to`), kullanıcı özelliği ile alınan `$to` ifade.</span><span class="sxs-lookup"><span data-stu-id="e08b7-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="e08b7-175">Köşeli ayraçlar kullanarak sistem özelliği her zaman erişebilirsiniz `{}`: ifade örneği için kullanabileceğiniz `{$to}` sistem özelliğine erişmek için `to`.</span><span class="sxs-lookup"><span data-stu-id="e08b7-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="e08b7-176">Köşeli parantez içindeki özellik adları, her zaman karşılık gelen sistem özelliği alır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="e08b7-177">Özellik adları büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e08b7-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="e08b7-178">Tüm ileti özellikleri dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-178">All message properties are strings.</span></span> <span data-ttu-id="e08b7-179">Bölümünde açıklandığı gibi sistem özelliklerini [Geliştirici Kılavuzu][lnk-devguide-messaging-format], şu anda sorgularında kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="e08b7-180">Örneğin, kullanırsanız, bir `messageType` özelliği, tüm telemetri bir uç nokta ve başka bir uç nokta için tüm uyarılar yönlendirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e08b7-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="e08b7-181">Telemetri yönlendirmek için aşağıdaki ifade yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e08b7-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="e08b7-182">Ve uyarı iletileri yönlendirmek için aşağıdaki ifade:</span><span class="sxs-lookup"><span data-stu-id="e08b7-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="e08b7-183">Boole ifadeleri ve işlevleri de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="e08b7-184">Bu özellik, örneğin önem düzeyi arasında ayrım sağlar:</span><span class="sxs-lookup"><span data-stu-id="e08b7-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="e08b7-185">Başvurmak [ifade ve koşullar] [ lnk-query-expressions] desteklenen işleçler ve işlevlerin tam listesi için bölümü.</span><span class="sxs-lookup"><span data-stu-id="e08b7-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="e08b7-186">İleti gövdeleri yönlendirme</span><span class="sxs-lookup"><span data-stu-id="e08b7-186">Routing on message bodies</span></span>

<span data-ttu-id="e08b7-187">IOT Hub, ileti gövdesinde dayalı yalnızca yönlendirebilirsiniz ileti gövdesi doğru ise, içeriği biçimlendirilmiş JSON UTF-8, UTF-16 veya UTF-32 kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="e08b7-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="e08b7-188">İletiye içerik türü ayarlamalısınız `application/json` ve IOT Hub'ı gövde içeriğine göre ileti yönlendirmek izin vermek için ileti üstbilgilerinde desteklenen UTF Kodlamalar birine içerik kodlaması.</span><span class="sxs-lookup"><span data-stu-id="e08b7-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="e08b7-189">Üstbilgileri birini belirtilmezse, IOT hub'ı karşı ileti gövdesi içeren herhangi bir sorgu ifade değerlendirmek çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="e08b7-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="e08b7-190">İletinizi bir JSON ileti değilse veya ileti içerik türü ve içerik kodlamasını belirtmiyorsa hala ileti yönlendirme iletisi başlıklarını temel ileti yönlendirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e08b7-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="e08b7-191">Kullanabileceğiniz `$body` ileti yönlendirmek için sorgu ifadesinde.</span><span class="sxs-lookup"><span data-stu-id="e08b7-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="e08b7-192">Sorgu ifadesinde basit gövde başvurusu, gövde dizi başvuru ya da birden fazla gövde başvuru kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e08b7-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="e08b7-193">Sorgu ifadesi ayrıca gövde başvuru iletisi başlığı başvurusu ile birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e08b7-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="e08b7-194">Örneğin, tüm geçerli sorgu ifadeleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e08b7-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="e08b7-195">IOT Hub sorgusuyla temelleri</span><span class="sxs-lookup"><span data-stu-id="e08b7-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="e08b7-196">Her IOT hub'ı sorgu seçme ve FROM yan tümcesi ve isteğe bağlı WHERE ve GROUP BY yan tümceleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="e08b7-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="e08b7-197">Her sorgu JSON belgeleri, örneğin cihaz çiftlerini topluluğu üzerinde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="e08b7-198">FROM yan tümcesi üzerinde yinelendiğinde için belge koleksiyonunu gösterir (**aygıtları** veya **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="e08b7-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="e08b7-199">Ardından, WHERE yan tümcesinde filtre uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="e08b7-200">Toplamalar ile bu adım olarak gruplandırılır GROUP BY yan tümcesinde ve her grup için belirtilen bir satır oluşturulan SELECT yan tümcesi belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="e08b7-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="e08b7-201">FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="e08b7-201">FROM clause</span></span>
<span data-ttu-id="e08b7-202">**< From_specification > gelen** yan tümcesi, yalnızca iki değer varsayabilirsiniz: **AYGITLARDAN**, cihaz çiftlerini sorgulamak veya **devices.jobs gelen**, işin cihaz başına sorgulamak için ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="e08b7-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="e08b7-203">WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="e08b7-203">WHERE clause</span></span>
<span data-ttu-id="e08b7-204">**Burada < filter_condition >** yan tümcesi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="e08b7-205">JSON FROM koleksiyonunda belgeleri bir veya daha fazla sonucunu bir parçası olarak dahil edilecek koşullarını gerekir belirtir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="e08b7-206">Herhangi bir JSON belge sonucu dahil edilecek "true" belirtilen koşulları değerlendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="e08b7-207">İzin verilen koşullar bölümünde açıklanan [ifadeleri ve koşullar][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="e08b7-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="e08b7-208">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="e08b7-208">SELECT clause</span></span>
<span data-ttu-id="e08b7-209">SELECT yan tümcesi (**seçin < select_list >**) zorunludur ve değerleri sorgudan alınan belirtir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="e08b7-210">Yeni JSON nesnelerini oluşturmak için kullanılacak JSON değerleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="e08b7-211">Her kaynak koleksiyonu filtrelenmiş (ve isteğe bağlı olarak gruplandırılmış) alt öğe için yansıtma aşaması SELECT yan tümcesinde belirtilen değerlerle oluşturulan yeni bir JSON nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e08b7-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="e08b7-212">SELECT yan tümcesi dilbilgisi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="e08b7-212">Following is the grammar of the SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="e08b7-213">Burada **attribute_name** FROM koleksiyonundaki JSON belgesinin herhangi bir özelliğe başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="e08b7-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="e08b7-214">SELECT yan tümceleri bazı örnekler bulunabilir [cihaz çifti sorguları ile çalışmaya başlama] [ lnk-query-getstarted] bölümü.</span><span class="sxs-lookup"><span data-stu-id="e08b7-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="e08b7-215">Şu anda, seçim yan tümceleri farklı **seçin \***  cihaz çiftlerini toplama sorgularında yalnızca desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="e08b7-216">GROUP BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="e08b7-216">GROUP BY clause</span></span>
<span data-ttu-id="e08b7-217">**GROUP BY < group_specification >** yan tümcesi WHERE yan tümcesinde ve SELECT belirtilen projeksiyon önce belirtilen filtre sonra yürütülen isteğe bağlı bir adım olan.</span><span class="sxs-lookup"><span data-stu-id="e08b7-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="e08b7-218">Bir özniteliğin değerine bağlı olarak belgelerin gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="e08b7-219">Bu gruplar, SELECT yan tümcesinde belirtilen toplanmış değerlerini oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="e08b7-220">GROUP BY kullanarak bir sorgu örneğidir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="e08b7-221">GROUP BY resmi sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="e08b7-222">Burada **attribute_name** FROM koleksiyonundaki JSON belgesinin herhangi bir özelliğe başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="e08b7-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="e08b7-223">Şu anda, GROUP BY yan tümcesi, yalnızca cihaz çiftlerini sorgulanırken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="e08b7-224">İfadeler ve koşullar</span><span class="sxs-lookup"><span data-stu-id="e08b7-224">Expressions and conditions</span></span>
<span data-ttu-id="e08b7-225">Yüksek bir düzeyde bir *ifade*:</span><span class="sxs-lookup"><span data-stu-id="e08b7-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="e08b7-226">(Örneğin, Boolean, sayı, dize, dizi veya nesne), JSON türünün bir örneği için değerlendirir ve</span><span class="sxs-lookup"><span data-stu-id="e08b7-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="e08b7-227">Cihaz JSON belgesi ve yerleşik işleçler ve işlevleri kullanarak sabitleri gelen veri düzenleme tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="e08b7-228">*Koşullar* bir Boole değeri değerlendirmek ifadeler.</span><span class="sxs-lookup"><span data-stu-id="e08b7-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="e08b7-229">Boole değeri'den farklı herhangi sabiti **true** olarak kabul **false** (dahil olmak üzere **null**, **tanımsız**, herhangi bir nesne veya dizi örneği, herhangi bir dize ve açıkça Boolean **false**).</span><span class="sxs-lookup"><span data-stu-id="e08b7-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="e08b7-230">İfadeler sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-230">The syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="e08b7-231">Burada:</span><span class="sxs-lookup"><span data-stu-id="e08b7-231">where:</span></span>

| <span data-ttu-id="e08b7-232">Simgesi</span><span class="sxs-lookup"><span data-stu-id="e08b7-232">Symbol</span></span> | <span data-ttu-id="e08b7-233">Tanım</span><span class="sxs-lookup"><span data-stu-id="e08b7-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="e08b7-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="e08b7-234">attribute_name</span></span> | <span data-ttu-id="e08b7-235">JSON belgesinde herhangi bir özelliği **FROM** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="e08b7-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="e08b7-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="e08b7-236">binary_operator</span></span> | <span data-ttu-id="e08b7-237">Listelenen herhangi bir ikili işleç [işleçleri](#operators) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e08b7-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="e08b7-238">işlev_adı</span><span class="sxs-lookup"><span data-stu-id="e08b7-238">function_name</span></span>| <span data-ttu-id="e08b7-239">Listelenen herhangi bir işlev [işlevleri](#functions) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e08b7-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="e08b7-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="e08b7-240">decimal_literal</span></span> |<span data-ttu-id="e08b7-241">Bir kayan noktalı ondalık gösterimde.</span><span class="sxs-lookup"><span data-stu-id="e08b7-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="e08b7-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="e08b7-242">hexadecimal_literal</span></span> |<span data-ttu-id="e08b7-243">'0 x onaltılık basamak dizesiyle ve ardından' dize olarak ifade edilen bir sayı.</span><span class="sxs-lookup"><span data-stu-id="e08b7-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="e08b7-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="e08b7-244">string_literal</span></span> |<span data-ttu-id="e08b7-245">Dize değişmez değerleri, sıfır veya daha fazla Unicode karakter dizisi veya kaçış sıraları tarafından temsil edilen Unicode dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="e08b7-246">Dize değişmez değerleri tek tırnak içine alınmış (kesme işareti: ') veya çift tırnak (tırnak işareti: ").</span><span class="sxs-lookup"><span data-stu-id="e08b7-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="e08b7-247">Çıkışları izin: `\'`, `\"`, `\\`, `\uXXXX` 4 onaltılık basamak tarafından tanımlanan Unicode karakterler.</span><span class="sxs-lookup"><span data-stu-id="e08b7-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="e08b7-248">İşleçler</span><span class="sxs-lookup"><span data-stu-id="e08b7-248">Operators</span></span>
<span data-ttu-id="e08b7-249">Aşağıdaki işleçleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-249">The following operators are supported:</span></span>

| <span data-ttu-id="e08b7-250">Ailesi</span><span class="sxs-lookup"><span data-stu-id="e08b7-250">Family</span></span> | <span data-ttu-id="e08b7-251">İşleçler</span><span class="sxs-lookup"><span data-stu-id="e08b7-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="e08b7-252">Aritmetik</span><span class="sxs-lookup"><span data-stu-id="e08b7-252">Arithmetic</span></span> |<span data-ttu-id="e08b7-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="e08b7-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="e08b7-254">Mantıksal</span><span class="sxs-lookup"><span data-stu-id="e08b7-254">Logical</span></span> |<span data-ttu-id="e08b7-255">VE VEYA DEĞİL</span><span class="sxs-lookup"><span data-stu-id="e08b7-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="e08b7-256">Karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="e08b7-256">Comparison</span></span> |<span data-ttu-id="e08b7-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="e08b7-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="e08b7-258">İşlevler</span><span class="sxs-lookup"><span data-stu-id="e08b7-258">Functions</span></span>
<span data-ttu-id="e08b7-259">Çiftlerini ve desteklenen tek işleri sorgulanırken işlevi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="e08b7-260">İşlevi</span><span class="sxs-lookup"><span data-stu-id="e08b7-260">Function</span></span> | <span data-ttu-id="e08b7-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e08b7-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="e08b7-262">IS_DEFINED(Property)</span><span class="sxs-lookup"><span data-stu-id="e08b7-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="e08b7-263">Özellik değeri atanmış olan gösteren bir Boole değeri döndürür (de dahil olmak üzere `null`).</span><span class="sxs-lookup"><span data-stu-id="e08b7-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="e08b7-264">Yollar koşullarında aşağıdaki matematik işlevleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="e08b7-265">İşlevi</span><span class="sxs-lookup"><span data-stu-id="e08b7-265">Function</span></span> | <span data-ttu-id="e08b7-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e08b7-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="e08b7-267">Abs(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-267">ABS(x)</span></span> | <span data-ttu-id="e08b7-268">Belirtilen sayısal ifade (pozitif) mutlak değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="e08b7-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-269">EXP(x)</span></span> | <span data-ttu-id="e08b7-270">Belirtilen sayısal ifade üstel değeri döndürür (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="e08b7-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="e08b7-271">Power(x,y)</span><span class="sxs-lookup"><span data-stu-id="e08b7-271">POWER(x,y)</span></span> | <span data-ttu-id="e08b7-272">Belirtilen güç belirtilen ifadenin değerini döndürür (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="e08b7-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="e08b7-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-273">SQUARE(x)</span></span> | <span data-ttu-id="e08b7-274">Kare belirtilen sayısal değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="e08b7-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-275">CEILING(x)</span></span> | <span data-ttu-id="e08b7-276">Büyüktür veya eşittir, belirtilen sayısal ifadenin en küçük tamsayı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="e08b7-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-277">FLOOR(x)</span></span> | <span data-ttu-id="e08b7-278">Belirtilen sayısal ifade küçük veya eşit en büyük tamsayıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="e08b7-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-279">SIGN(x)</span></span> | <span data-ttu-id="e08b7-280">Artı (+ 1), sıfır (0) veya belirtilen sayısal ifadenin eksi (-1) işareti döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="e08b7-281">Sqrt(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-281">SQRT(x)</span></span> | <span data-ttu-id="e08b7-282">Kare belirtilen sayısal değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="e08b7-283">Yollar koşullarda, aşağıdaki tür denetleme ve atama işlevleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="e08b7-284">İşlevi</span><span class="sxs-lookup"><span data-stu-id="e08b7-284">Function</span></span> | <span data-ttu-id="e08b7-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e08b7-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="e08b7-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="e08b7-286">AS_NUMBER</span></span> | <span data-ttu-id="e08b7-287">Giriş dizesini sayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-287">Converts the input string to a number.</span></span> <span data-ttu-id="e08b7-288">`noop`Giriş bir sayı ise; `Undefined` dize bir sayıyı temsil etmiyor durumunda.</span><span class="sxs-lookup"><span data-stu-id="e08b7-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="e08b7-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="e08b7-289">IS_ARRAY</span></span> | <span data-ttu-id="e08b7-290">Belirtilen ifade türü bir dizi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="e08b7-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="e08b7-291">IS_BOOL</span></span> | <span data-ttu-id="e08b7-292">Belirtilen ifade türü bir Boole değeri olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="e08b7-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="e08b7-293">IS_DEFINED</span></span> | <span data-ttu-id="e08b7-294">Özellik değeri atanmış olan gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="e08b7-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="e08b7-295">IS_NULL</span></span> | <span data-ttu-id="e08b7-296">Belirtilen ifade türü null olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="e08b7-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="e08b7-297">IS_NUMBER</span></span> | <span data-ttu-id="e08b7-298">Belirtilen ifade türü bir sayı olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="e08b7-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="e08b7-299">IS_OBJECT</span></span> | <span data-ttu-id="e08b7-300">Belirtilen ifade türü bir JSON nesnesi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="e08b7-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="e08b7-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="e08b7-302">Belirtilen ifade türü bir basit tür olup olmadığını gösteren bir Boole değeri döndürür (dize, Boolean, sayısal veya `null`).</span><span class="sxs-lookup"><span data-stu-id="e08b7-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="e08b7-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="e08b7-303">IS_STRING</span></span> | <span data-ttu-id="e08b7-304">Belirtilen ifade türü bir dize olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="e08b7-305">Yollar koşullarında aşağıdaki dize işlevleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e08b7-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="e08b7-306">İşlevi</span><span class="sxs-lookup"><span data-stu-id="e08b7-306">Function</span></span> | <span data-ttu-id="e08b7-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e08b7-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="e08b7-308">CONCAT(x,...)</span><span class="sxs-lookup"><span data-stu-id="e08b7-308">CONCAT(x, …)</span></span> | <span data-ttu-id="e08b7-309">İki veya daha fazla dize değerlerini birleştirme sonucu olan bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="e08b7-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-310">LENGTH(x)</span></span> | <span data-ttu-id="e08b7-311">Belirtilen dize ifadesinin karakterlerin sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="e08b7-312">Lower(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-312">LOWER(x)</span></span> | <span data-ttu-id="e08b7-313">Büyük harf karakter verileri küçük harfe dönüştürmek sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="e08b7-314">Upper(x)</span><span class="sxs-lookup"><span data-stu-id="e08b7-314">UPPER(x)</span></span> | <span data-ttu-id="e08b7-315">Küçük harf karakter verileri büyük harfe dönüştürme sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e08b7-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="e08b7-316">SUBSTRING (dize, başlangıç [, uzunluk])</span><span class="sxs-lookup"><span data-stu-id="e08b7-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="e08b7-317">Belirtilen karakter sıfır tabanlı konumdan başlayarak bir dize ifadesi bölümünü döndürür ve belirtilen uzunlukta veya dize sonu devam eder.</span><span class="sxs-lookup"><span data-stu-id="e08b7-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="e08b7-318">INDEX_OF (dize, parça)</span><span class="sxs-lookup"><span data-stu-id="e08b7-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="e08b7-319">İkinci ilk örneğinin başlangıç konumunu döndürür dizesi ifade ilk belirtilen dize ifadesi veya -1 içinde dizesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="e08b7-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="e08b7-320">STARTS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="e08b7-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="e08b7-321">Döndüren bir Boolean belirten ilk ifade dize olup olmadığını ve ikinci başlatır.</span><span class="sxs-lookup"><span data-stu-id="e08b7-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="e08b7-322">ENDS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="e08b7-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="e08b7-323">Döndürür Boolean belirten bir ilk ifade dize olup olmadığını ve ikinci sona erer.</span><span class="sxs-lookup"><span data-stu-id="e08b7-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="e08b7-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="e08b7-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="e08b7-325">Döndüren bir Boolean belirten ikinci ilk ifade dize olup olmadığını içerir.</span><span class="sxs-lookup"><span data-stu-id="e08b7-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e08b7-326">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e08b7-326">Next steps</span></span>
<span data-ttu-id="e08b7-327">Sorguları kullanarak uygulamalarınızı yürütün öğrenin [Azure IOT SDK'ları][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="e08b7-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
