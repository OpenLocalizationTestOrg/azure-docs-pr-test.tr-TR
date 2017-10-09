---
title: aaaUnderstand hello Azure IOT Hub sorgu dili | Microsoft Docs
description: "Geliştirici Kılavuzu - hello SQL benzeri IOT hub'ı sorgu dili açıklaması cihaz çiftlerini ve IOT hub'ınızı işlerden hakkında tooretrieve bilgi kullanılır."
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
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="9c3d1-103">Başvuru - cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili</span><span class="sxs-lookup"><span data-stu-id="9c3d1-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="9c3d1-104">IOT hub'ı güçlü SQL benzeri bir dil tooretrieve bilgilerini sağlamaktadır ilgili [cihaz çiftlerini] [ lnk-twins] ve [işleri][lnk-jobs]ve [ileti yönlendirme][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="9c3d1-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="9c3d1-105">Bu makalede sunar:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-105">This article presents:</span></span>

* <span data-ttu-id="9c3d1-106">Bir giriş toohello ana özelliklerini hello IOT hub'ı sorgu dili ve</span><span class="sxs-lookup"><span data-stu-id="9c3d1-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="9c3d1-107">Merhaba hello dil açıklaması ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="9c3d1-108">Cihaz çifti sorguları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c3d1-108">Get started with device twin queries</span></span>
<span data-ttu-id="9c3d1-109">[Cihaz çiftlerini] [ lnk-twins] etiketleri ve özellikleri rastgele JSON nesnelerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="9c3d1-110">IOT Hub, tooquery cihaz çiftlerini tüm cihaz çifti bilgilerini içeren tek bir JSON belgesi olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="9c3d1-111">Örneğin, IOT hub cihaz çiftlerini yapı izlenerek hello olduğunu varsayın:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

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

<span data-ttu-id="9c3d1-112">IOT hub'ı sunan hello cihaz çiftlerini adlı bir belge koleksiyonu olarak **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="9c3d1-113">Bu nedenle sorgu aşağıdaki hello hello tüm cihaz çiftlerini kümesini alır:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="9c3d1-114">[Azure IOT SDK'ları] [ lnk-hub-sdks] büyük sonuçlarının disk belleği destekler.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="9c3d1-115">IOT Hub ile rastgele koşullar filtreleme tooretrieve cihaz çiftlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="9c3d1-116">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="9c3d1-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="9c3d1-117">alır hello cihaz çiftlerini ile Merhaba **location.region** etiketi ayarlayın çok**ABD**.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="9c3d1-118">Boole işleçleri ve aritmetik karşılaştırmaları de, örneğin desteklenir</span><span class="sxs-lookup"><span data-stu-id="9c3d1-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="9c3d1-119">Merhaba BİZE yapılandırılmış toosend telemetri değerinden genellikle dakikada bulunan tüm cihaz çiftlerini alır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="9c3d1-120">Kolaylık, aynı zamanda hello ile olası toouse dizi sabitleri olup **IN** ve **NBU** (içinde değil) işleçler.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="9c3d1-121">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="9c3d1-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="9c3d1-122">WiFi bildirilen veya bağlantı kablolu tüm cihaz çiftlerini alır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="9c3d1-123">Bu genellikle gerekli tooidentify belirli bir özellik içeren tüm cihaz çiftlerini değil.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="9c3d1-124">IOT hub'ı destekleyen hello işlevi `is_defined()` bu amaç için.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="9c3d1-125">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="9c3d1-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="9c3d1-126">Merhaba tanımlamak tüm cihaz çiftlerini alınan `connectivity` özelliği bildirdi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="9c3d1-127">Toohello başvuran [WHERE yan tümcesi] [ lnk-query-where] filtreleme özellikleri hello hello tam başvuru için bölüm.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="9c3d1-128">Gruplandırma ve toplamalar da desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="9c3d1-129">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="9c3d1-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="9c3d1-130">Merhaba cihaz Hello sayısı her telemetri yapılandırma durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="9c3d1-131">Merhaba önceki örnekte burada üç aygıt başarılı bir yapılandırma bildirilen, iki hala hello yapılandırmayı uygulama ve bir hata bildirdi bir durum gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="9c3d1-132">C# örnek</span><span class="sxs-lookup"><span data-stu-id="9c3d1-132">C# example</span></span>
<span data-ttu-id="9c3d1-133">Merhaba sorgu işlevi hello tarafından sunulan [C# hizmeti SDK'sını] [ lnk-hub-sdks] hello içinde **RegistryManager** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="9c3d1-134">Burada, basit bir sorgu örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="9c3d1-135">Not nasıl hello **sorgu** nesne örneği içeren bir sayfa boyutuna (yukarı too1000) ve ardından birden çok sayfa arama hello tarafından alınabilecek **GetNextAsTwinAsync** yöntemleri birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="9c3d1-136">Bu hello sorgu nesneyi kullanıma sunan birden çok Not **sonraki\***, cihaz çifti ya da iş nesneleri gibi hello sorgu gerektirdiği hello seri durumdan çıkarma seçeneği veya tahminleri kullanılırken düz JSON toobe bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="9c3d1-137">Node.js örneği</span><span class="sxs-lookup"><span data-stu-id="9c3d1-137">Node.js example</span></span>
<span data-ttu-id="9c3d1-138">Merhaba sorgu işlevi hello tarafından sunulan [Node.js için Azure IOT hizmeti SDK'sını] [ lnk-hub-sdks] hello içinde **kayıt defteri** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="9c3d1-139">Burada, basit bir sorgu örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
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

<span data-ttu-id="9c3d1-140">Not nasıl hello **sorgu** nesne örneği içeren bir sayfa boyutuna (yukarı too1000) ve ardından birden çok sayfa arama hello tarafından alınabilecek **nextAsTwin** yöntemleri birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="9c3d1-141">Bu hello sorgu nesneyi kullanıma sunan birden çok Not **sonraki\***, cihaz çifti ya da iş nesneleri gibi hello sorgu gerektirdiği hello seri durumdan çıkarma seçeneği veya tahminleri kullanılırken düz JSON toobe bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="9c3d1-142">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="9c3d1-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9c3d1-143">Sorgu sonuçları gecikme saygı toohello en son değerleri ile birkaç dakika içinde cihaz çiftlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="9c3d1-144">Tek tek cihaz çiftlerini kimliğine göre sorgulama, her zaman tercih toouse hello varsa, her zaman hello en son değerleri içerir ve daha yüksek azaltma sınırları cihaz çifti API alın.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="9c3d1-145">Şu anda karşılaştırmaları yalnızca ilkel türler arasında (hiçbir nesne), örneğin desteklenir `... WHERE properties.desired.config = properties.reported.config` yalnızca bu özellikleri ilkel değerler varsa desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="9c3d1-146">İşlerini sorguları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c3d1-146">Get started with jobs queries</span></span>
<span data-ttu-id="9c3d1-147">[İşlerini] [ lnk-jobs] şekilde tooexecute aygıtları kümesi üzerinde işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="9c3d1-148">Her cihaz çifti onu olduğu adlı bir koleksiyon bölümünde hello işleri hello bilgileri içeren **işleri**.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="9c3d1-149">Mantıksal olarak</span><span class="sxs-lookup"><span data-stu-id="9c3d1-149">Logically,</span></span>

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

<span data-ttu-id="9c3d1-150">Bu koleksiyon şu anda olarak sorgulanabilir **devices.jobs** hello IOT hub'ı sorgu dili içinde.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c3d1-151">Şu anda hello işleri özelliği, hiçbir zaman cihaz çiftlerini (diğer bir deyişle, 'aygıtlardan' içeren sorgular) sorgulanırken döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="9c3d1-152">Yalnızca doğrudan sorgu kullanarak erişilebilir `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="9c3d1-153">Örneğin, tooget tek bir cihazı etkileyen tüm işleri (Geçmiş ve zamanlanmış), sorgu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="9c3d1-154">Bu sorgu hello cihaza özel durumu (ve büyük olasılıkla hello doğrudan yöntemi yanıtı) döndürülen her bir iş nasıl sağladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="9c3d1-155">Aynı zamanda tüm nesne özellikleri hello içinde rastgele Boolean koşullarla olası toofilter olan **devices.jobs** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="9c3d1-156">Örneğin, sorgu hello:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="9c3d1-157">Tüm tamamlanan alır cihaz çifti güncelleştirme işleri aygıtın **myDeviceId** Eylül 2016 sonra oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="9c3d1-158">Ayrıca olası tooretrieve hello aygıt başına sonuçlarını tek bir işi yerdir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="9c3d1-159">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="9c3d1-159">Limitations</span></span>
<span data-ttu-id="9c3d1-160">Üzerinde şu anda sorgular **devices.jobs** desteklemez:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="9c3d1-161">Projeksiyonlar, bu nedenle yalnızca `SELECT *` mümkündür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="9c3d1-162">Toplama toojob özellikleri (önceki bölümde hello bakın) toohello cihaz çiftine başvuran koşulları.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="9c3d1-163">Count, avg, grupla gibi toplamalar gerçekleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="9c3d1-164">Cihaz bulut ileti yollar sorgu ifadeleri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c3d1-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="9c3d1-165">Kullanarak [cihaz bulut yolları][lnk-devguide-messaging-routes], IOT Hub'ın toodispatch cihaz-bulut iletileri karşı tek bir ileti hesaplanan ifadeleri göre toodifferent uç noktalarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="9c3d1-166">Merhaba rota [koşulu] [ lnk-query-expressions] hello aynı IOT hub'ı sorgu dili twin ve iş sorguları koşullarında olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="9c3d1-167">Yol koşulları hello ileti üstbilgilerini ve gövde değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="9c3d1-168">Yönlendirme sorgu ifadesi yalnızca hello ileti gövdesi, yalnızca ileti üstbilgilerini gerektirebilir veya her ikisi de üstbilgileri iletisi ve ileti gövdesi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="9c3d1-169">IOT hub'ı hello üstbilgiler ve ileti gövdesini sipariş tooroute iletileri için belirli bir şema olduğu varsayılır ve IOT hub'ı tooproperly rotası için gerekli olan bölümleri aşağıdaki hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="9c3d1-170">İleti üstbilgilerinde yönlendirme</span><span class="sxs-lookup"><span data-stu-id="9c3d1-170">Routing on message headers</span></span>

<span data-ttu-id="9c3d1-171">IOT hub'ı ileti yönlendirme için ileti üstbilgilerini JSON gösterimi aşağıdaki hello varsayılır:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="9c3d1-172">İleti sistemi özellikleri ile Merhaba önekli `'$'` simgesi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="9c3d1-173">Kullanıcı özellikleri her zaman kendi adıyla erişilir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="9c3d1-174">Bir kullanıcı özellik adı bir sistem özelliğiyle toocoincide ortaya çıkarsa (gibi `$to`), hello kullanıcı özelliği ile Merhaba alınan `$to` ifade.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="9c3d1-175">Köşeli ayraçlar kullanan hello sistem özellik her zaman erişebilirsiniz `{}`: hello ifade örneği için kullanabileceğiniz `{$to}` tooaccess hello sistem özelliği `to`.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="9c3d1-176">Köşeli parantez içindeki özellik adları daima hello karşılık gelen sistem özelliği alır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="9c3d1-177">Özellik adları büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="9c3d1-178">Tüm ileti özellikleri dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-178">All message properties are strings.</span></span> <span data-ttu-id="9c3d1-179">Hello açıklandığı gibi sistem özelliklerini [Geliştirici Kılavuzu][lnk-devguide-messaging-format], şu anda kullanılabilir toouse sorgularda değildir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="9c3d1-180">Örneğin, kullanırsanız, bir `messageType` özelliği, tüm telemetri tooone endpoint ve tüm uyarıları tooanother uç tooroute isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="9c3d1-181">İfade tooroute hello telemetri aşağıdaki hello yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="9c3d1-182">Ve ifade tooroute hello uyarı iletileri hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="9c3d1-183">Boole ifadeleri ve işlevleri de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="9c3d1-184">Bu özellik, toodistinguish önem düzeyi arasında örneğin sağlar:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="9c3d1-185">Toohello başvuran [ifade ve koşullar] [ lnk-query-expressions] bölümünü hello tam listesi için desteklenen işleçleri ve işlevleri.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="9c3d1-186">İleti gövdeleri yönlendirme</span><span class="sxs-lookup"><span data-stu-id="9c3d1-186">Routing on message bodies</span></span>

<span data-ttu-id="9c3d1-187">IOT Hub, ileti gövdesinde dayalı yalnızca yönlendirebilirsiniz hello ileti gövdesi doğru ise, içeriği biçimlendirilmiş JSON UTF-8, UTF-16 veya UTF-32 kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="9c3d1-188">Merhaba iletisinin hello içerik türü çok ayarlamalısınız`application/json` ve hello içerik kodlama tooone Merhaba, IOT hub'ı tooroute selamlama iletisine hello gövde içeriğine göre hello ileti üstbilgilerini tooallow UTF Kodlamalar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="9c3d1-189">Merhaba üstbilgileri birini belirtilmezse, IOT hub'ı hello gövde selamlama iletisine karşı içeren herhangi bir sorgu ifade tooevaluate denemez.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="9c3d1-190">İleti bir JSON ileti değilse veya selamlama iletisine hello içerik türü ve içerik kodlamasını belirtmiyorsa, ileti tooroute selamlama iletisine hello ileti üstbilgilerinde tabanlı yönlendirme hala kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="9c3d1-191">Kullanabileceğiniz `$body` hello sorgu ifadesi tooroute Başlangıç iletisi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="9c3d1-192">Basit gövde başvurusu, gövde dizi başvuru ya da birden fazla gövde başvuru hello sorgu ifadesinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="9c3d1-193">Sorgu ifadesi ayrıca gövde başvuru iletisi başlığı başvurusu ile birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="9c3d1-194">Örneğin, tüm geçerli sorgu ifadeleri hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="9c3d1-195">IOT Hub sorgusuyla temelleri</span><span class="sxs-lookup"><span data-stu-id="9c3d1-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="9c3d1-196">Her IOT hub'ı sorgu seçme ve FROM yan tümcesi ve isteğe bağlı WHERE ve GROUP BY yan tümceleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="9c3d1-197">Her sorgu JSON belgeleri, örneğin cihaz çiftlerini topluluğu üzerinde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="9c3d1-198">Merhaba FROM yan tümcesi üzerinde yinelendiğinde hello belge koleksiyonu toobe gösterir (**aygıtları** veya **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="9c3d1-199">Ardından, burada yan tümcesi uygulanır hello filtrede hello.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="9c3d1-200">Toplamalar ile bu adımı hello sonuçlarını GROUP BY yan tümcesi içinde belirtilen hello gruplandırılır ve her grup için bir satır oluşturulur hello SELECT yan tümcesinde belirtilen.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="9c3d1-201">FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-201">FROM clause</span></span>
<span data-ttu-id="9c3d1-202">Merhaba **< from_specification > gelen** yan tümcesi, yalnızca iki değer varsayabilirsiniz: **AYGITLARDAN**, tooquery cihaz çiftlerini veya **devices.jobs gelen**, tooquery işi cihaz başına Ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="9c3d1-203">WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-203">WHERE clause</span></span>
<span data-ttu-id="9c3d1-204">Merhaba **burada < filter_condition >** yan tümcesi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="9c3d1-205">Merhaba JSON belgelerini hello FROM koleksiyonundaki hello sonuç bir parçası olarak dahil edilen toobe getirmelidir bir veya daha fazla koşulları belirtir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="9c3d1-206">Herhangi bir JSON belge değerlendirilmelidir hello belirtilen koşullar çok "true" Merhaba sonucunda içerilen toobe.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="9c3d1-207">Merhaba izin koşulları bölümünde açıklanan [ifadeleri ve koşullar][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="9c3d1-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="9c3d1-208">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-208">SELECT clause</span></span>
<span data-ttu-id="9c3d1-209">Merhaba SELECT yan tümcesi (**seçin < select_list >**) zorunludur ve hangi değerlerin hello sorgudan alınan belirtir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="9c3d1-210">Merhaba JSON değerleri toobe toogenerate yeni JSON nesnelerinin kullanılan belirtir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="9c3d1-211">Her öğe için filtrelenmiş (ve isteğe bağlı olarak gruplandırılmış) alt hello FROM koleksiyonunun Merhaba, hello projeksiyon aşaması hello SELECT yan tümcesinde belirtilen hello değerlerle oluşturulan yeni bir JSON nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="9c3d1-212">Merhaba SELECT yan tümcesi hello dilbilgisi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-212">Following is hello grammar of hello SELECT clause:</span></span>

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

<span data-ttu-id="9c3d1-213">Burada **attribute_name** tooany özelliği hello JSON belgesinin hello FROM koleksiyonundaki başvurur.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="9c3d1-214">SELECT yan tümceleri bazı örnekleri hello bulunabilir [cihaz çifti sorguları ile çalışmaya başlama] [ lnk-query-getstarted] bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="9c3d1-215">Şu anda, seçim yan tümceleri farklı **seçin \***  cihaz çiftlerini toplama sorgularında yalnızca desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="9c3d1-216">GROUP BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-216">GROUP BY clause</span></span>
<span data-ttu-id="9c3d1-217">Merhaba **GROUP BY < group_specification >** yan tümcesi hello filtre hello WHERE yan tümcesinde belirtilen sonra çalıştırılabilir ve hello belirtilen hello projeksiyon önce seçin isteğe bağlı bir adım olan.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="9c3d1-218">Belgeleri bir özniteliğin hello değere göre gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="9c3d1-219">Bu gruplar, hello SELECT yan tümcesinde belirtilen toplanan kullanılan toogenerate değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="9c3d1-220">GROUP BY kullanarak bir sorgu örneğidir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="9c3d1-221">Merhaba resmi için GROUP BY söz dizimi:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="9c3d1-222">Burada **attribute_name** tooany özelliği hello JSON belgesinin hello FROM koleksiyonundaki başvurur.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="9c3d1-223">Şu anda hello GROUP BY yan tümcesi, yalnızca cihaz çiftlerini sorgulanırken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="9c3d1-224">İfadeler ve koşullar</span><span class="sxs-lookup"><span data-stu-id="9c3d1-224">Expressions and conditions</span></span>
<span data-ttu-id="9c3d1-225">Yüksek bir düzeyde bir *ifade*:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="9c3d1-226">Bir JSON türü (örneğin, Boolean, sayı, dize, dizi veya nesne), tooan örneği değerlendirir ve</span><span class="sxs-lookup"><span data-stu-id="9c3d1-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="9c3d1-227">Merhaba aygıt JSON belgesi ve yerleşik işleçler ve işlevleri kullanarak sabitleri gelen veri düzenleme tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="9c3d1-228">*Koşullar* tooa Boolean değerlendirmek ifadeler.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="9c3d1-229">Boolean farklı herhangi sabiti **true** olarak kabul **false** (dahil olmak üzere **null**, **tanımsız**, tüm nesne veya dizi örneği Tüm dize ve açıkça hello Boolean **false**).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="9c3d1-230">ifadeler Hello sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-230">hello syntax for expressions is:</span></span>

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

<span data-ttu-id="9c3d1-231">Burada:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-231">where:</span></span>

| <span data-ttu-id="9c3d1-232">Simgesi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-232">Symbol</span></span> | <span data-ttu-id="9c3d1-233">Tanım</span><span class="sxs-lookup"><span data-stu-id="9c3d1-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="9c3d1-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="9c3d1-234">attribute_name</span></span> | <span data-ttu-id="9c3d1-235">Merhaba hello JSON belgesinde herhangi bir özelliği **FROM** koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="9c3d1-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="9c3d1-236">binary_operator</span></span> | <span data-ttu-id="9c3d1-237">Herhangi bir ikili işleç listelenen hello [işleçleri](#operators) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="9c3d1-238">işlev_adı</span><span class="sxs-lookup"><span data-stu-id="9c3d1-238">function_name</span></span>| <span data-ttu-id="9c3d1-239">Herhangi bir işlev listelenen hello [işlevleri](#functions) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="9c3d1-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="9c3d1-240">decimal_literal</span></span> |<span data-ttu-id="9c3d1-241">Bir kayan noktalı ondalık gösterimde.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="9c3d1-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="9c3d1-242">hexadecimal_literal</span></span> |<span data-ttu-id="9c3d1-243">Bir sayı '0 x onaltılık basamak dizesiyle ve ardından' hello dizesiyle ifade.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="9c3d1-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="9c3d1-244">string_literal</span></span> |<span data-ttu-id="9c3d1-245">Dize değişmez değerleri, sıfır veya daha fazla Unicode karakter dizisi veya kaçış sıraları tarafından temsil edilen Unicode dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="9c3d1-246">Dize değişmez değerleri tek tırnak içine alınmış (kesme işareti: ') veya çift tırnak (tırnak işareti: ").</span><span class="sxs-lookup"><span data-stu-id="9c3d1-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="9c3d1-247">Çıkışları izin: `\'`, `\"`, `\\`, `\uXXXX` 4 onaltılık basamak tarafından tanımlanan Unicode karakterler.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="9c3d1-248">İşleçler</span><span class="sxs-lookup"><span data-stu-id="9c3d1-248">Operators</span></span>
<span data-ttu-id="9c3d1-249">işleçler aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-249">hello following operators are supported:</span></span>

| <span data-ttu-id="9c3d1-250">Ailesi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-250">Family</span></span> | <span data-ttu-id="9c3d1-251">İşleçler</span><span class="sxs-lookup"><span data-stu-id="9c3d1-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="9c3d1-252">Aritmetik</span><span class="sxs-lookup"><span data-stu-id="9c3d1-252">Arithmetic</span></span> |<span data-ttu-id="9c3d1-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="9c3d1-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="9c3d1-254">Mantıksal</span><span class="sxs-lookup"><span data-stu-id="9c3d1-254">Logical</span></span> |<span data-ttu-id="9c3d1-255">VE VEYA DEĞİL</span><span class="sxs-lookup"><span data-stu-id="9c3d1-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="9c3d1-256">Karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="9c3d1-256">Comparison</span></span> |<span data-ttu-id="9c3d1-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="9c3d1-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="9c3d1-258">İşlevler</span><span class="sxs-lookup"><span data-stu-id="9c3d1-258">Functions</span></span>
<span data-ttu-id="9c3d1-259">Yalnızca desteklenen çiftlerini ve işleri hello sorgulanırken işlevi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="9c3d1-260">İşlevi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-260">Function</span></span> | <span data-ttu-id="9c3d1-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9c3d1-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c3d1-262">IS_DEFINED(Property)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="9c3d1-263">Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür (de dahil olmak üzere `null`).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="9c3d1-264">Yollar koşullarında matematik işlevleri aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="9c3d1-265">İşlevi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-265">Function</span></span> | <span data-ttu-id="9c3d1-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9c3d1-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c3d1-267">Abs(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-267">ABS(x)</span></span> | <span data-ttu-id="9c3d1-268">Sayısal ifade döndürür hello mutlak (pozitif) değerini hello belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="9c3d1-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-269">EXP(x)</span></span> | <span data-ttu-id="9c3d1-270">Merhaba, hello üstel değer döndüren belirtilen sayısal ifade (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="9c3d1-271">Power(x,y)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-271">POWER(x,y)</span></span> | <span data-ttu-id="9c3d1-272">Döndürür hello belirtilen başlangıç değeri ifadesi toohello belirtilen güç (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="9c3d1-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-273">SQUARE(x)</span></span> | <span data-ttu-id="9c3d1-274">Merhaba kare döndürür hello sayısal değer belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="9c3d1-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-275">CEILING(x)</span></span> | <span data-ttu-id="9c3d1-276">En küçük tamsayı değeri büyük hello veya belirtilen sayısal ifade hello eşit verir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="9c3d1-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-277">FLOOR(x)</span></span> | <span data-ttu-id="9c3d1-278">Daha az Hello en büyük tamsayıyı döndürür veya bu değere eşit toohello sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="9c3d1-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-279">SIGN(x)</span></span> | <span data-ttu-id="9c3d1-280">Artı (+ 1), sıfır (0), döndürür hello veya sayısal ifade hello eksi (-1) belirtisi belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="9c3d1-281">Sqrt(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-281">SQRT(x)</span></span> | <span data-ttu-id="9c3d1-282">Merhaba kare döndürür hello sayısal değer belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="9c3d1-283">Yollar koşullarında denetleme ve işlevleri atama türü aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="9c3d1-284">İşlevi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-284">Function</span></span> | <span data-ttu-id="9c3d1-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9c3d1-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c3d1-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="9c3d1-286">AS_NUMBER</span></span> | <span data-ttu-id="9c3d1-287">Merhaba giriş dizesi tooa sayıyı dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="9c3d1-288">`noop`Giriş bir sayı ise; `Undefined` dize bir sayıyı temsil etmiyor durumunda.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="9c3d1-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="9c3d1-289">IS_ARRAY</span></span> | <span data-ttu-id="9c3d1-290">Bir dizidir hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="9c3d1-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="9c3d1-291">IS_BOOL</span></span> | <span data-ttu-id="9c3d1-292">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="9c3d1-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="9c3d1-293">IS_DEFINED</span></span> | <span data-ttu-id="9c3d1-294">Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="9c3d1-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="9c3d1-295">IS_NULL</span></span> | <span data-ttu-id="9c3d1-296">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri null döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="9c3d1-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="9c3d1-297">IS_NUMBER</span></span> | <span data-ttu-id="9c3d1-298">Bir sayıdır hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="9c3d1-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="9c3d1-299">IS_OBJECT</span></span> | <span data-ttu-id="9c3d1-300">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir JSON nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="9c3d1-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="9c3d1-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="9c3d1-302">Merhaba Hello türü ifade ilkel belirtilirse, gösteren bir Boole değeri döndürür (dize, Boolean, sayısal veya `null`).</span><span class="sxs-lookup"><span data-stu-id="9c3d1-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="9c3d1-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="9c3d1-303">IS_STRING</span></span> | <span data-ttu-id="9c3d1-304">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri bir dize verir.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="9c3d1-305">Yollar koşullarında dize işlevleri aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="9c3d1-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="9c3d1-306">İşlevi</span><span class="sxs-lookup"><span data-stu-id="9c3d1-306">Function</span></span> | <span data-ttu-id="9c3d1-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9c3d1-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c3d1-308">CONCAT(x,...)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-308">CONCAT(x, …)</span></span> | <span data-ttu-id="9c3d1-309">İki veya daha fazla dize değerlerini birleştirme hello sonucu olan bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="9c3d1-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-310">LENGTH(x)</span></span> | <span data-ttu-id="9c3d1-311">Dize ifadesi belirtilen döndürür hello hello karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="9c3d1-312">Lower(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-312">LOWER(x)</span></span> | <span data-ttu-id="9c3d1-313">Büyük harf karakter veri toolowercase dönüştürmeden sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="9c3d1-314">Upper(x)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-314">UPPER(x)</span></span> | <span data-ttu-id="9c3d1-315">Küçük harf karakter veri toouppercase dönüştürmeden sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="9c3d1-316">SUBSTRING (dize, başlangıç [, uzunluk])</span><span class="sxs-lookup"><span data-stu-id="9c3d1-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="9c3d1-317">Merhaba başlayan bir dize ifadesi döndürür parçası karakter sıfır tabanlı konumu belirtilen ve uzunluk veya hello dize toohello sonu toohello belirtilen devam eder.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="9c3d1-318">INDEX_OF (dize, parça)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="9c3d1-319">Merhaba dize bulunmazsa hello ikinci dize ifadesi hello ilk belirtilen dize ifadesi veya -1 içinde hello ilk oluşum konumunu başlangıç hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="9c3d1-320">STARTS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="9c3d1-321">Merhaba ilk dize ifadesi ile Merhaba ikinci başlayıp başlamadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="9c3d1-322">ENDS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="9c3d1-323">Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="9c3d1-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="9c3d1-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="9c3d1-325">Merhaba ilk dize ifadesi hello ikinci içerip içermediğini gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c3d1-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c3d1-326">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c3d1-326">Next steps</span></span>
<span data-ttu-id="9c3d1-327">Tooexecute kullanarak uygulamalarınızı nasıl sorgular öğrenin [Azure IOT SDK'ları][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="9c3d1-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
