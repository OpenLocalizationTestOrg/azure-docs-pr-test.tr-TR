---
title: "Bir Azure zaman serisi Öngörüler ortama olayları göndermek nasıl | Microsoft Docs"
description: "Bu öğretici, oluşturmak, olay hub'ı yapılandırmak ve Azure zaman serisi Insights'ta gösterilmesini itme olaylara bir örnek uygulamayı çalıştırın açıklanmaktadır."
services: time-series-insights
ms.service: time-series-insights
author: venkatgct
ms.author: venkatja
manager: jhubbard
editor: MarkMcGeeAtAquent
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.devlang: csharp
ms.workload: big-data
ms.topic: article
ms.date: 11/15/2017
ms.openlocfilehash: 2c1b91fb87857eee8ca938be193b61e01bbdb886
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/16/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a>Olay hub’ı kullanarak olayları Zaman Serisi Görüşleri ortamına gönderme
Bu makalede oluşturmak ve olay hub'ı yapılandırmak nasıl açıklar ve anında iletme olaylara bir örnek uygulamayı çalıştırın. Varolan bir event hub'olaylarla JSON biçiminde varsa, Bu öğretici atlayın ve ortamınızdaki görüntülemek [zaman serisi Öngörüler](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Olay hub’ını yapılandırma
1. Olay hub’ı oluşturmak için, Olay Hub’ı [belgelerindeki](../event-hubs/event-hubs-create.md) yönergeleri izleyin.

2. Arama **olay hub'ı** arama çubuğunda. Tıklatın **olay hub'ları** döndürülen listedeki.

3. Olay hub'ınızı adına tıklayarak seçin.

4. Altında **varlıklar** Orta yapılandırma penceresinde **olay hub'ları** yeniden.

5. Olay hub'ı yapılandırmak için adını seçin.

  ![Olay hub’ı tüketici grubunu seçme](media/send-events/consumer-group.png)

6. Altında **varlıklar**seçin **tüketici grupları**.
 
7. Özel olarak yalnızca Zaman Serisi Görüşleri olay kaynağınız tarafından kullanılan bir tüketici grubu oluşturduğunuzdan emin olun.

   > [!IMPORTANT]
   > Bu tüketici grubunun başka hiçbir hizmet (örneğin, Stream Analytics işi veya başka bir Zaman Serisi Görüşleri ortamı) tarafından kullanılmadığından emin olun. Tüketici grubu tarafından kullanılıyorsa, hizmetleri, okuma işlemi olumsuz şekilde etkilenir bu ortam ve diğer hizmetler için. Tüketici grubu olarak “$Default” kullanıyorsanız, bu diğer okuyucular tarafından olası yeniden kullanıma yol açabilir.

8. Altında **ayarları** başlığını seçin **paylaşım erişim ilkeleri**.

9. Olay hub'ına, oluşturma **MySendPolicy** csharp örnek olayları göndermek için kullanılır.

  ![Paylaşılan erişim ilkeleri’ni seçin ve Ekle düğmesine tıklayın](media/send-events/shared-access-policy.png)  

  ![Yeni paylaşılan erişim ilkesi ekleme](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Zaman Serisi Görüşleri olay kaynağı oluşturma
1. Bir olay kaynağı oluşturmadıysanız, olay kaynağını oluşturmak için [bu yönergeleri](time-series-insights-how-to-add-an-event-source-eventhub.md) izleyin.

2. Belirtin **deviceTimestamp** zaman damgası özellik adı olarak – bu özellik C# örnek gerçek zaman damgası olarak kullanılır. Zaman damgası özellik adı büyük/küçük harfe duyarlıdır ve olay hub’ına JSON olarak gönderildiğinde değerleri __yyyy-AA-ggTSS:dd:ss.FFFFFFFK__ biçiminde olmalıdır. Özellik olayda mevcut değilse olay hub'ı sıraya alınan zamanı kullanılır.

  ![Olay kaynağı oluşturma](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a>Olayları göndermek için kullanılacak örnek kod
1. Adlı bir olay hub'ı ilke gidin **MySendPolicy**. Kopya **bağlantı dizesi** İlkesi anahtara sahip.

  ![MySendPolicy bağlantı dizesini kopyalama](media/send-events/sample-code-connection-string.png)

2. Üç cihazdan her biri için 600 olay gönderecek olan aşağıdaki kodu çalıştırın. `eventHubConnectionString` öğesini bağlantı dizenizle güncelleştirin.

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

                // Send JSON to event hub.
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
İki JSON nesnesi içeren JSON dizisi. Her JSON nesnesi bir olaya dönüştürülür.
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
"location" özelliğinin her olaya kopyalandığına dikkat edin.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|cihaz1|2016-01-08T01:08:00Z|
|WestUs|cihaz2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Örnek 4

#### <a name="input"></a>Girdi

İki JSON nesnesi içeren iç içe bir JSON dizisi ile JSON nesnesi. Girilen bu değer, genel özelliklerin karmaşık JSON nesnesiyle ifade edilebileceğini gösterir.

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
> [!div class="nextstepaction"]
> [Zaman serisi Öngörüler Explorer'da ortamınızı görüntülemek](https://insights.timeseries.azure.com).
