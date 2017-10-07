---
title: "aaaGet başlatılan Azure IOT hub'ı (.NET) | Microsoft Docs"
description: "Nasıl tooAzure IOT Hub'ın IOT SDK'ları için .NET kullanarak toosend cihaz-bulut iletileri öğrenin. Sanal cihazı ve hizmet uygulamaları tooregister Cihazınızı oluşturmak, iletileri gönderir ve IOT hub'ından iletileri okur."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>.NET kullanarak aygıt tooyour IOT hub'ınıza bağlanın

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Bu öğretici Hello sonunda üç .NET konsol uygulamaları vardır:

* **CreateDeviceIdentity**ilişkili güvenlik anahtarı tooconnect cihaz uygulamanız ve bir cihaz kimliği oluşturur.
* **ReadDeviceToCloudMessages**, cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.
* **SimulatedDevice**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello MQTT protokolünü kullanarak her saniye bir telemetri iletisi gönderir.

Github'dan hello üç uygulamaları içeren hello Visual Studio çözümü kopyalama veya indirilir.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Cihazlardaki uygulamalar toorun hem, çözüm arka ucu hello Azure IOT SDK'ları hakkında toobuild kullanabileceğiniz bilgi için bkz [Azure IOT SDK'ları][lnk-hub-sdks].

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

IOT hub'ınızı oluşturdunuz ve hello ana bilgisayar adı ve IOT Hub bağlantı dizesine toocomplete hello Bu öğreticinin geri kalanını gerek yoktur.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Cihazdan buluta iletileri alma
Bu bölümde IoT Hub'dan cihaz-bulut iletilerini okuyan bir .NET konsol uygulaması oluşturacaksınız. IOT hub'ı kullanıma sunan bir [Azure Event Hubs][lnk-event-hubs-overview]-uyumlu bir uç noktasını tooenable, tooread cihaz bulut iletilerini. tookeep şeyler basit, Bu öğretici, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur. tooprocess cihaz-bulut iletileri ölçekli olarak nasıl toolearn bakın hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi. Merhaba nasıl tooprocess olay hub'larından iletileri hakkında daha fazla bilgi için bkz: [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Öğreticisi. (Bu öğretici geçerli toohello IOT Hub ve Event Hub ile uyumlu uç noktaları olur.)

> [!NOTE]
> Merhaba cihaz bulut iletilerini her zaman okumak için Event Hub ile uyumlu uç nokta hello AMQP protokolünü kullanır.

1. Visual Studio'da bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme, hello kullanarak ekleyin **konsol uygulaması (.NET Framework)** proje şablonu. Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü. Ad hello proje **ReadDeviceToCloudMessages**.

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10a]

2. Çözüm Gezgini'nde hello sağ **ReadDeviceToCloudMessages** proje ve ardından **NuGet paketlerini Yönet**.

3. Merhaba, **NuGet Paket Yöneticisi** penceresinde, arama **WindowsAzure.ServiceBus**seçin **yükleme**ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve bir başvuru çok ekler[Azure Service Bus][lnk-servicebus-nuget], tüm bağımlılıklarıyla birlikte. Bu paket hello uygulama tooconnect toohello Event Hub ile uyumlu uç IOT hub'ınızı sağlar.

4. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba hello "IOT hub oluşturma" bölümünde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    Bu yöntem bir **EventHubReceiver** örneği tooreceive tüm hello IOT hub'a cihaz-bulut iletileri alma bölümlerinden. Nasıl geçirdiğinize dikkat edin bir `DateTime.Now` hello oluşturduğunuzda parametresi **EventHubReceiver** yalnızca başladıktan sonra gönderilen iletileri alması nesne. Merhaba geçerli iletiler kümesini görebileceğiniz için bu filtre bir test ortamında kullanışlıdır. Bir üretim ortamında kodunuzun tüm hello iletileri işlediğinden emin olmanız gerekir. Merhaba öğretici daha fazla bilgi için bkz [nasıl tooprocess IOT Hub cihaz bulut iletilerini][lnk-process-d2c-tutorial].

7. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a>Cihaz uygulaması oluşturma

Bu bölümde, tooan IOT hub'ı cihaz-bulut iletileri gönderen bir cihaza benzetim yapan bir .NET konsol uygulaması oluşturun.

1. Visual Studio'da bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme, hello kullanarak ekleyin **konsol uygulaması (.NET Framework)** proje şablonu. Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü. Ad hello proje **SimulatedDevice**.

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10b]

2. Çözüm Gezgini'nde hello sağ **SimulatedDevice** proje ve ardından **NuGet paketlerini Yönet**.

3. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **Microsoft.Azure.Devices.Client**seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı NuGet paketi] [ lnk-device-nuget] ve bağımlılıklarını.

4. Merhaba aşağıdakileri ekleyin `using` deyimi hello hello üstündeki **Program.cs** dosyası:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Yedek `{iot hub hostname}` hello IOT hub ana bilgisayar adıyla hello "IOT hub oluşturma" bölümünde alınır. Yedek `{device key}` hello aygıt anahtarı ile hello "bir cihaz kimliği oluşturma" bölümünde aldığınız.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    Bu yöntem, her saniye yeni bir cihazdan buluta iletisi gönderir. Selamlama iletisine ve rastgele sayılar toosimulate sıcaklık algılayıcısı ve nem algılayıcı oluşturulan hello cihaz kimliği ile JSON seri hale getirilmiş bir nesneyi içerir.

7. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    Varsayılan olarak, hello **oluşturma** yöntemi bir .NET Framework uygulamasında oluşturur bir **DeviceClient** IOT Hub ile Merhaba AMQP protokolünü toocommunicate kullanan örneği. toouse hello MQTT veya HTTP protokolünü kullanmak hello hello geçersiz kılma **oluşturma** toospecify hello Protokolü sağlar yöntemi. UWP ve PCL istemcileri varsayılan olarak hello HTTP protokolünü kullanır. Merhaba HTTP protokolü kullanırsanız, hello de eklemeniz gerekir **Microsoft.AspNet.WebApi.Client** NuGet paketi tooyour proje tooinclude hello **Microsoft.ASPNET.webapi.Client** ad alanı.

Bu öğretici hello adımları toocreate IOT hub'ı cihaz uygulaması gösterir. Merhaba de kullanabilirsiniz [Azure IOT Hub için bağlı hizmet] [ lnk-connected-service] Visual Studio uzantısı tooadd hello gerekli kodu tooyour cihaz uygulaması.

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello uygulamaları sunulmuştur.

1. Visual Studio'daki Çözüm Gezgini'nde çözümünüze sağ tıklayın ve ardından **Başlangıç projelerini ayarla**'ya tıklayın. Seçin **birden fazla başlangıç projesi**ve ardından **Başlat** hem hello hello eylem olarak **ReadDeviceToCloudMessages** ve **SimulatedDevice** projeleri.

    ![Başlangıç projesinin özellikleri][41]

2. Tuşuna **F5** toostart çalışan her iki uygulamalar. Merhaba hello konsol çıktısı **SimulatedDevice** uygulama gösterir Merhaba iletileri tooyour IOT hub cihaz uygulamanız gönderir. Merhaba hello konsol çıktısı **ReadDeviceToCloudMessages** uygulama IOT hub'ınızın aldığı hello iletileri gösterir.

    ![Uygulamalardan konsol çıktısı][42]

3. Merhaba **kullanım** döşeme hello [Azure portal] [ lnk-portal] gösterir hello gönderilen iletileri toohello IOT hub'ı sayısı:

    ![Azure portalı Kullanım kutucuğu][43]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir IOT hub'hello Azure portal yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Bu cihaz kimliğini tooenable hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır. Merhaba hello IOT hub tarafından alınan iletileri görüntüleyen bir uygulama da oluşturmuş.

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

* [Cihazınızı bağlama][lnk-connect-device]
* [Cihaz yönetimini kullanmaya başlama][lnk-device-management]
* [IoT Edge ile çalışmaya başlama][lnk-iot-edge]

toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
