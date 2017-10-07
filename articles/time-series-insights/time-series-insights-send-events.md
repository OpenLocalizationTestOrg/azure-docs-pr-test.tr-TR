---
title: "aaaSend olayları tooAzure zaman serisi Öngörüler ortamı | Microsoft Docs"
description: "Bu öğretici hello adımları toopush olayları tooyour zaman serisi Öngörüler ortamı kapsar"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="7d07a-103">Olay hub'ı kullanarak olayları tooa zaman serisi Öngörüler ortamı Gönder</span><span class="sxs-lookup"><span data-stu-id="7d07a-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="7d07a-104">Bu öğretici açıklar nasıl toocreate olay hub'ı yapılandırmak ve bir örnek uygulama toopush olayları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7d07a-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="7d07a-105">JSON biçiminde olaylar içeren bir olay hub’ınız mevcutsa bu öğreticiyi atlayabilir ve [zaman serisi görüşlerinde](https://insights.timeseries.azure.com) ortamınızı görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d07a-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="7d07a-106">Olay hub’ını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7d07a-106">Configure an event hub</span></span>
1. <span data-ttu-id="7d07a-107">toocreate bir event hub olay hub'ı hello yönergeleri izleyerek [belgelerine](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="7d07a-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="7d07a-108">Özel olarak yalnızca Zaman Serisi Görüşleri olay kaynağınız tarafından kullanılan bir tüketici grubu oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7d07a-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7d07a-109">Bu tüketici grubunun başka hiçbir hizmet (örneğin, Stream Analytics işi veya başka bir Zaman Serisi Görüşleri ortamı) tarafından kullanılmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7d07a-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="7d07a-110">Bir tüketici grubundaki diğer hizmetler tarafından kullanılıyorsa, işlem olumsuz bu ortam için etkilenen okuyun ve diğer hizmetleri hello.</span><span class="sxs-lookup"><span data-stu-id="7d07a-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="7d07a-111">"$Default" Merhaba tüketici grubu olarak kullanıyorsanız, diğer okuyucular tarafından toopotential yeniden yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="7d07a-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Olay hub’ı tüketici grubunu seçme](media/send-events/consumer-group.png)

3. <span data-ttu-id="7d07a-113">"MySendPolicy" Merhaba olay hub'ına, oluşturma diğer bir deyişle hello csharp örnek kullanılan toosend olaylar.</span><span class="sxs-lookup"><span data-stu-id="7d07a-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Paylaşılan erişim ilkeleri’ni seçin ve Ekle düğmesine tıklayın](media/send-events/shared-access-policy.png)  

  ![Yeni paylaşılan erişim ilkesi ekleme](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="7d07a-116">Zaman Serisi Görüşleri olay kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d07a-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="7d07a-117">Bir olay kaynağı oluşturmadıysanız, izleyin [bu yönergeleri](time-series-insights-add-event-source.md) toocreate bir olay kaynağı.</span><span class="sxs-lookup"><span data-stu-id="7d07a-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="7d07a-118">"DeviceTimestamp" Merhaba zaman damgası özelliği adı olarak belirtmeniz – bu özellik, gerçek zaman damgası hello csharp örneği'nde hello olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d07a-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="7d07a-119">Merhaba zaman damgası özelliği adı büyük küçük harfe duyarlı ve değerleri hello biçimi izlemelidir __yyyy-MM-ddTHH. FFFFFFFK__ JSON tooevent hub olarak gönderildiğinde.</span><span class="sxs-lookup"><span data-stu-id="7d07a-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="7d07a-120">Merhaba özelliği hello olayda mevcut değilse daha sonra hello olay hub'ı sıraya alınan zaman kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d07a-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Olay kaynağı oluşturma](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="7d07a-122">Örnek kod toopush olaylar</span><span class="sxs-lookup"><span data-stu-id="7d07a-122">Sample code toopush events</span></span>
1. <span data-ttu-id="7d07a-123">Toohello olay hub'ı İlkesi "MySendPolicy" gidin ve hello İlkesi anahtarla hello bağlantı dizesini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7d07a-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![MySendPolicy bağlantı dizesini kopyalama](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="7d07a-125">Koddan hello her hello üç aygıtların toosend 600 olayların çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7d07a-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="7d07a-126">`eventHubConnectionString` öğesini bağlantı dizenizle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7d07a-126">Update `eventHubConnectionString` with your connection string.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="7d07a-127">Desteklenen JSON şekilleri</span><span class="sxs-lookup"><span data-stu-id="7d07a-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="7d07a-128">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="7d07a-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="7d07a-129">Girdi</span><span class="sxs-lookup"><span data-stu-id="7d07a-129">Input</span></span>

<span data-ttu-id="7d07a-130">Basit bir JSON nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7d07a-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="7d07a-131">Çıkış - 1 olay</span><span class="sxs-lookup"><span data-stu-id="7d07a-131">Output - 1 event</span></span>

|<span data-ttu-id="7d07a-132">id</span><span class="sxs-lookup"><span data-stu-id="7d07a-132">id</span></span>|<span data-ttu-id="7d07a-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="7d07a-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="7d07a-134">cihaz1</span><span class="sxs-lookup"><span data-stu-id="7d07a-134">device1</span></span>|<span data-ttu-id="7d07a-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7d07a-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="7d07a-136">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="7d07a-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="7d07a-137">Girdi</span><span class="sxs-lookup"><span data-stu-id="7d07a-137">Input</span></span>
<span data-ttu-id="7d07a-138">İki JSON nesnesi içeren JSON dizisi.</span><span class="sxs-lookup"><span data-stu-id="7d07a-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="7d07a-139">Her bir JSON nesnesi dönüştürülmüş tooan olay olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d07a-139">Each JSON object will be converted tooan event.</span></span>
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a><span data-ttu-id="7d07a-140">Çıkış - 2 Olay</span><span class="sxs-lookup"><span data-stu-id="7d07a-140">Output - 2 Events</span></span>

|<span data-ttu-id="7d07a-141">id</span><span class="sxs-lookup"><span data-stu-id="7d07a-141">id</span></span>|<span data-ttu-id="7d07a-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="7d07a-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="7d07a-143">cihaz1</span><span class="sxs-lookup"><span data-stu-id="7d07a-143">device1</span></span>|<span data-ttu-id="7d07a-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7d07a-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="7d07a-145">cihaz2</span><span class="sxs-lookup"><span data-stu-id="7d07a-145">device2</span></span>|<span data-ttu-id="7d07a-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="7d07a-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="7d07a-147">Örnek 3</span><span class="sxs-lookup"><span data-stu-id="7d07a-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="7d07a-148">Girdi</span><span class="sxs-lookup"><span data-stu-id="7d07a-148">Input</span></span>

<span data-ttu-id="7d07a-149">İki JSON nesnesi içeren iç içe bir JSON dizisi ile JSON nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7d07a-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a><span data-ttu-id="7d07a-150">Çıkış - 2 Olay</span><span class="sxs-lookup"><span data-stu-id="7d07a-150">Output - 2 Events</span></span>
<span data-ttu-id="7d07a-151">Merhaba özelliği "Konum" Merhaba olay tooeach kopyalanır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7d07a-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="7d07a-152">location</span><span class="sxs-lookup"><span data-stu-id="7d07a-152">location</span></span>|<span data-ttu-id="7d07a-153">events.id</span><span class="sxs-lookup"><span data-stu-id="7d07a-153">events.id</span></span>|<span data-ttu-id="7d07a-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="7d07a-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="7d07a-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="7d07a-155">WestUs</span></span>|<span data-ttu-id="7d07a-156">cihaz1</span><span class="sxs-lookup"><span data-stu-id="7d07a-156">device1</span></span>|<span data-ttu-id="7d07a-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7d07a-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="7d07a-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="7d07a-158">WestUs</span></span>|<span data-ttu-id="7d07a-159">cihaz2</span><span class="sxs-lookup"><span data-stu-id="7d07a-159">device2</span></span>|<span data-ttu-id="7d07a-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="7d07a-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="7d07a-161">Örnek 4</span><span class="sxs-lookup"><span data-stu-id="7d07a-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="7d07a-162">Girdi</span><span class="sxs-lookup"><span data-stu-id="7d07a-162">Input</span></span>

<span data-ttu-id="7d07a-163">İki JSON nesnesi içeren iç içe bir JSON dizisi ile JSON nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7d07a-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="7d07a-164">Bu giriş hello genel özellikleri hello karmaşık JSON nesnesi tarafından temsil edilebilir olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d07a-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a><span data-ttu-id="7d07a-165">Çıkış - 2 Olay</span><span class="sxs-lookup"><span data-stu-id="7d07a-165">Output - 2 Events</span></span>

|<span data-ttu-id="7d07a-166">location</span><span class="sxs-lookup"><span data-stu-id="7d07a-166">location</span></span>|<span data-ttu-id="7d07a-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="7d07a-167">manufacturer.name</span></span>|<span data-ttu-id="7d07a-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="7d07a-168">manufacturer.location</span></span>|<span data-ttu-id="7d07a-169">events.id</span><span class="sxs-lookup"><span data-stu-id="7d07a-169">events.id</span></span>|<span data-ttu-id="7d07a-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="7d07a-170">events.timestamp</span></span>|<span data-ttu-id="7d07a-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="7d07a-171">events.data.type</span></span>|<span data-ttu-id="7d07a-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="7d07a-172">events.data.units</span></span>|<span data-ttu-id="7d07a-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="7d07a-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="7d07a-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="7d07a-174">WestUs</span></span>|<span data-ttu-id="7d07a-175">üretici1</span><span class="sxs-lookup"><span data-stu-id="7d07a-175">manufacturer1</span></span>|<span data-ttu-id="7d07a-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="7d07a-176">EastUs</span></span>|<span data-ttu-id="7d07a-177">cihaz1</span><span class="sxs-lookup"><span data-stu-id="7d07a-177">device1</span></span>|<span data-ttu-id="7d07a-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7d07a-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="7d07a-179">basınç</span><span class="sxs-lookup"><span data-stu-id="7d07a-179">pressure</span></span>|<span data-ttu-id="7d07a-180">psi</span><span class="sxs-lookup"><span data-stu-id="7d07a-180">psi</span></span>|<span data-ttu-id="7d07a-181">108.09</span><span class="sxs-lookup"><span data-stu-id="7d07a-181">108.09</span></span>|
|<span data-ttu-id="7d07a-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="7d07a-182">WestUs</span></span>|<span data-ttu-id="7d07a-183">üretici1</span><span class="sxs-lookup"><span data-stu-id="7d07a-183">manufacturer1</span></span>|<span data-ttu-id="7d07a-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="7d07a-184">EastUs</span></span>|<span data-ttu-id="7d07a-185">cihaz2</span><span class="sxs-lookup"><span data-stu-id="7d07a-185">device2</span></span>|<span data-ttu-id="7d07a-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="7d07a-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="7d07a-187">titreşim</span><span class="sxs-lookup"><span data-stu-id="7d07a-187">vibration</span></span>|<span data-ttu-id="7d07a-188">abs G</span><span class="sxs-lookup"><span data-stu-id="7d07a-188">abs G</span></span>|<span data-ttu-id="7d07a-189">217.09</span><span class="sxs-lookup"><span data-stu-id="7d07a-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="7d07a-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d07a-190">Next steps</span></span>

* <span data-ttu-id="7d07a-191">[Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="7d07a-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
