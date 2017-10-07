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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Olay hub'ı kullanarak olayları tooa zaman serisi Öngörüler ortamı Gönder

Bu öğretici açıklar nasıl toocreate olay hub'ı yapılandırmak ve bir örnek uygulama toopush olayları çalıştırın. JSON biçiminde olaylar içeren bir olay hub’ınız mevcutsa bu öğreticiyi atlayabilir ve [zaman serisi görüşlerinde](https://insights.timeseries.azure.com) ortamınızı görüntüleyebilirsiniz.

## <a name="configure-an-event-hub"></a>Olay hub’ını yapılandırma
1. toocreate bir event hub olay hub'ı hello yönergeleri izleyerek [belgelerine](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Özel olarak yalnızca Zaman Serisi Görüşleri olay kaynağınız tarafından kullanılan bir tüketici grubu oluşturduğunuzdan emin olun.

  > [!IMPORTANT]
  > Bu tüketici grubunun başka hiçbir hizmet (örneğin, Stream Analytics işi veya başka bir Zaman Serisi Görüşleri ortamı) tarafından kullanılmadığından emin olun. Bir tüketici grubundaki diğer hizmetler tarafından kullanılıyorsa, işlem olumsuz bu ortam için etkilenen okuyun ve diğer hizmetleri hello. "$Default" Merhaba tüketici grubu olarak kullanıyorsanız, diğer okuyucular tarafından toopotential yeniden yol açabilir.

  ![Olay hub’ı tüketici grubunu seçme](media/send-events/consumer-group.png)

3. "MySendPolicy" Merhaba olay hub'ına, oluşturma diğer bir deyişle hello csharp örnek kullanılan toosend olaylar.

  ![Paylaşılan erişim ilkeleri’ni seçin ve Ekle düğmesine tıklayın](media/send-events/shared-access-policy.png)  

  ![Yeni paylaşılan erişim ilkesi ekleme](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Zaman Serisi Görüşleri olay kaynağı oluşturma
1. Bir olay kaynağı oluşturmadıysanız, izleyin [bu yönergeleri](time-series-insights-add-event-source.md) toocreate bir olay kaynağı.

2. "DeviceTimestamp" Merhaba zaman damgası özelliği adı olarak belirtmeniz – bu özellik, gerçek zaman damgası hello csharp örneği'nde hello olarak kullanılır. Merhaba zaman damgası özelliği adı büyük küçük harfe duyarlı ve değerleri hello biçimi izlemelidir __yyyy-MM-ddTHH. FFFFFFFK__ JSON tooevent hub olarak gönderildiğinde. Merhaba özelliği hello olayda mevcut değilse daha sonra hello olay hub'ı sıraya alınan zaman kullanılır.

  ![Olay kaynağı oluşturma](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Örnek kod toopush olaylar
1. Toohello olay hub'ı İlkesi "MySendPolicy" gidin ve hello İlkesi anahtarla hello bağlantı dizesini kopyalayın.

  ![MySendPolicy bağlantı dizesini kopyalama](media/send-events/sample-code-connection-string.png)

2. Koddan hello her hello üç aygıtların toosend 600 olayların çalıştırın. `eventHubConnectionString` öğesini bağlantı dizenizle güncelleştirin.

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
## <a name="supported-json-shapes"></a>Desteklenen JSON şekilleri
### <a name="sample-1"></a>Örnek 1

#### <a name="input"></a>Girdi

Basit bir JSON nesnesi.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Çıkış - 1 olay

|id|timestamp|
|--------|---------------|
|cihaz1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Örnek 2

#### <a name="input"></a>Girdi
İki JSON nesnesi içeren JSON dizisi. Her bir JSON nesnesi dönüştürülmüş tooan olay olacaktır.
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
#### <a name="output---2-events"></a>Çıkış - 2 Olay

|id|timestamp|
|--------|---------------|
|cihaz1|2016-01-08T01:08:00Z|
|cihaz2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>Örnek 3

#### <a name="input"></a>Girdi

İki JSON nesnesi içeren iç içe bir JSON dizisi ile JSON nesnesi.
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
#### <a name="output---2-events"></a>Çıkış - 2 Olay
Merhaba özelliği "Konum" Merhaba olay tooeach kopyalanır unutmayın.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|cihaz1|2016-01-08T01:08:00Z|
|WestUs|cihaz2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Örnek 4

#### <a name="input"></a>Girdi

İki JSON nesnesi içeren iç içe bir JSON dizisi ile JSON nesnesi. Bu giriş hello genel özellikleri hello karmaşık JSON nesnesi tarafından temsil edilebilir olduğunu gösterir.

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
#### <a name="output---2-events"></a>Çıkış - 2 Olay

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|üretici1|EastUs|cihaz1|2016-01-08T01:08:00Z|basınç|psi|108.09|
|WestUs|üretici1|EastUs|cihaz2|2016-01-08T01:17:00Z|titreşim|abs G|217.09|

## <a name="next-steps"></a>Sonraki adımlar

* [Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme
