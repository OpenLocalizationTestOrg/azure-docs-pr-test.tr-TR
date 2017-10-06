---
title: "İzleme aaaAzure IOT hub'ı operations | Microsoft Docs"
description: "Nasıl toomonitor izleme toouse Azure IOT Hub işlemleri gerçek zamanlı IOT hub'ınızı işlemlerinin durumunu hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>IOT hub'ı işlemlerini izleme

IOT hub'ı operations izleme toomonitor hello durumunu gerçek zamanlı IOT hub'ınızı işlemlerinin sağlar. IOT hub'ı operations birkaç kategoriler arasında olayları izler. IOT hub'ınızın işlemek için bir veya daha fazla kategorileri tooan uç noktasından olayları göndermeyi seçebilirsiniz. Merhaba veri hataları izleme veya veri düzenlerini esas alarak daha karmaşık işleme ayarlayın.

IOT hub'ı olayların altı kategoriye izler:

* Aygıt Kimliği işlemleri
* Cihaz telemetrisi
* Bulut-cihaz iletilerini
* Bağlantılar
* Dosya yüklemeleri
* İleti yönlendirme

## <a name="how-tooenable-operations-monitoring"></a>Nasıl tooenable işlemlerini izleme

1. IOT hub'ı oluşturun. Hakkında yönergeler bulabilirsiniz toocreate bir IOT hub'hello [Get Started] [ lnk-get-started] Kılavuzu.

1. IOT hub'ınızı Hello dikey penceresini açın. Buradan, tıklatın **izleme işlemleri**.

    ![Merhaba portalındaki izleme erişim işlemleri][1]

1. Select hello toomonitor ister ve ardından kategorileri izleme **kaydetmek**. Merhaba olayları listelenen hello Event Hub ile uyumlu uç noktasından okumak için kullanılabilir **izleme ayarlarını**. Merhaba IOT hub'ı uç adlandırılır `messages/operationsmonitoringevents`.

    ![IOT hub'ınızı üzerinde izleme işlemlerini yapılandırma][2]

> [!NOTE]
> Seçme **ayrıntılı** Merhaba izleme **bağlantıları** kategori toogenerate ek tanılama iletilerini IOT Hub neden olur. Diğer tüm kategorileri için hello **ayrıntılı** değişiklikleri bilgi IOT hub'ı hello miktarını ayarlama her hata iletisi içerir.

## <a name="event-categories-and-how-toouse-them"></a>Olay kategorileri ve nasıl toouse bunları

Her kategori parçaları izleme işlemleri farklı türde bir IOT Hub ve her izleme kategorisi etkileşimi bu kategorideki olayları nasıl yapılandırıldığı tanımlayan bir şema sahiptir.

### <a name="device-identity-operations"></a>Aygıt Kimliği işlemleri

Merhaba aygıt kimlik işlemleri kategorisini toocreate çalıştığınızda oluşan hataları izler, güncelleştirmek ya da, IOT hub'ın kimlik kayıt defterinde bir girişi silmek. Bu kategori izleme senaryoları sağlamak için kullanışlıdır.

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>Cihaz telemetrisi

Merhaba cihaz telemetri kategorisini hello IOT hub'ına oluşur ve ilgili toohello telemetri ardışık düzen hatalarını izler. Bu kategori (örneğin, azaltma) telemetri olayları gönderirken oluşan hataları içeren ve telemetri olayları (örneğin, yetkisiz okuyucu) alma. Bu kategori hello cihazının kendisinde çalışan kodu nedeni hatalarını yakalama olamaz.

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>Bulut cihaz komutları

Merhaba bulut-cihaz komutlarını kategori hello IOT hub'ına oluşur ve ilgili toohello bulut cihaz ileti işlem hattını hataları izler. Bu kategori (örneğin, yetkisiz gönderen) bulut cihaza ileti gönderme, (örneğin, teslimat sayısı aşıldı) bulut-cihaz iletilerini alma ve bulut-cihaz ileti geri bildirim (görüş süresi gibi) alırken oluşan hataları içerir. Bu kategori hello bulut aygıt iletisi başarılı bir şekilde teslim, yanlış bir bulut cihaz iletiyi işleyen bir aygıtı hatalarından yakalamaz.

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>Bağlantılar

Merhaba bağlantıları kategorisi cihazlar bağlanmak veya IOT hub'ından bağlantısını oluşan hataları izler. Bu kategori izleme, yetkisiz bağlantı denemeleri tanımlamak için ve zamanlar zayıf bağlantıya alanlarında cihazlar için bir bağlantı kesildiğinde izlemek için yararlıdır.

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>Dosya yüklemeleri

Merhaba dosya karşıya yükleme kategori hello IOT hub'ına oluşur ve ilgili toofile karşıya yükleme işlevselliği olan hataları izler. Bu kategori içerir:

* Merhaba hub tamamlanan karşıya yükleme, bir cihaz bildirir önce onu süresi dolduğunda gibi hello SAS URI'si ile oluşan hatalar.
* Merhaba cihaz tarafından raporlanan yüklemeler başarısız oldu.
* Bir dosya depolama alanına IOT hub'ı bildirim iletisi oluşturma sırasında bulunamadı kullanırken oluşan hatalar.

Bu kategori hello aygıt dosya toostorage karşıya doğrudan oluşan hatalar catch olamaz.

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>İleti yönlendirme

Merhaba ileti yönlendirme kategorisi ileti rota değerlendirme ve IOT Hub tarafından algılanan gibi uç noktası sistem durumu sırasında oluşan hataları izler. Bir kural "tanımsız" çok değerlendirildiğinde zaman IOT hub'ı bir uç nokta olarak atılacak ve bir uç noktasından alınan hatalarını işaretler gibi bu kategoriyi olaylarını içerir. Bu kategori hello "cihaz telemetrisi" kategorisi altında bildirilen hello iletilerini kendileri (örneğin, aygıt) hataları azaltma hakkında belirli hataları içermez.

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>Etkinlikleri görüntüleme

Merhaba kullanabilirsiniz *iothub-explorer* aracı tooquickly test IOT hub'ınızı izleme olayı oluşturuyor. tooinstall hello aracı, hello hello yönergelerini görmek [iothub-explorer] [ lnk-iothub-explorer] GitHub depo.

1. Merhaba emin olun **bağlantıları** kategori izleme ayarlanmış çok**ayrıntılı** hello Portalı'nda.

1. Bir komut isteminde, uç nokta izleme hello komutu tooread aşağıdaki hello çalıştırın:

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. Başka bir komut isteminden komut toosimulate aşağıdaki hello cihaz-bulut iletileri gönderen bir aygıt çalıştırın:

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. Merhaba sanal cihaz tooyour IOT hub'a bağlandığında hello ilk komut istemi hello izleme olayları gösterir.

## <a name="connect-toohello-monitoring-endpoint"></a>Uç nokta izleme toohello Bağlan

IOT hub'ınızı noktadaki izleme hello bir Event Hub ile uyumlu uç noktadır. Bu uç noktasından olay hub'ları tooread izleme iletileri ile birlikte çalışan herhangi bir mekanizma kullanabilirsiniz. Merhaba aşağıdaki örnek, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur. Merhaba nasıl tooprocess olay hub'larından iletileri hakkında daha fazla bilgi için bkz: [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Öğreticisi.

tooconnect toohello izleme uç noktası, bir bağlantı dizesi ve hello uç nokta adı gerekir. Aşağıdaki adımları hello nasıl toofind hello hello Portalı'nda gerekli değerleri göster:

1. Merhaba Portalı'nda tooyour IOT hub'ı kaynak dikey penceresine gidin.

1. Seçin **izleme işlemleri**ve hello Not **Event Hub ile uyumlu adı** ve **Event Hub ile uyumlu uç nokta** değerler:

    ![Olay Hub ile uyumlu uç nokta değerleri][img-endpoints]

1. Seçin **paylaşılan erişim ilkeleri**, ardından **hizmet**. Merhaba Not **birincil anahtar** değeri:

    ![Hizmet paylaşılan erişim ilkesi birincil anahtarı][img-service-key]

Merhaba aşağıdaki C# kod örneği Visual Studio'dan alınır **Windows Klasik Masaüstü** C# konsol uygulaması. Merhaba proje sahip hello **WindowsAzure.ServiceBus** NuGet paketi yüklü.

* Merhaba bağlantı dizesi yer tutucusunu hello kullanan bir bağlantı dizesi ile değiştirin **Event Hub ile uyumlu uç nokta** ve hizmet **birincil anahtar** hello aşağıda gösterildiği gibi daha önce not ettiğiniz değerleri Örnek:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Uç nokta ad yer tutucusu hello ile izleme hello yerine **Event Hub ile uyumlu adı** daha önce not ettiğiniz değer.

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md