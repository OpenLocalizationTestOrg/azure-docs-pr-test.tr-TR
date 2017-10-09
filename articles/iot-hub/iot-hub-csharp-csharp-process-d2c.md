---
title: "yollar (.Net) kullanılarak aaaProcess Azure IOT Hub cihaz bulut iletilerini | Microsoft Docs"
description: "Nasıl tooprocess yönlendirme kuralları ve özel uç noktaları toodispatch kullanarak IOT Hub cihaz bulut iletilerini tooother arka uç hizmetlerini iletileri."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Yollar (.NET) kullanılarak IOT Hub cihaz bulut iletilerini işleme

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Bu öğretici üzerinde hello derlemeler [IOT Hub ile çalışmaya başlama] Öğreticisi. Başlangıç Öğreticisi:

* Nasıl toouse yönlendirme toodispatch cihaz bulut iletilerini bir kolay, yapılandırma tabanlı şekilde kuralları gösterir.
* Nasıl hello çözümden Acil eylem gerektiren tooisolate etkileşimli iletilerin arka uç başka bir işleme için gösterilmektedir. Örneğin, bir aygıt bir bilet bir CRM sistemine ekleme tetikleyen bir uyarı iletisi gönderebilir. Buna karşılık, sıcaklık telemetri gibi veri noktası iletileri analytics motoruna akış.

Bu öğretici Hello sonunda üç .NET konsol uygulamaları çalıştırın:

* **SimulatedDevice**, hello oluşturulan hello uygulaması değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama] öğretici saniyede veri noktası cihaz bulut iletilerini gönderir ve etkileşimli cihaz bulut iletilerini her 10 saniye sayısı.
* **ReadDeviceToCloudMessages** görüntüler cihaz uygulamanız tarafından gönderilen kritik olmayan telemetri hello.
* **ReadCriticalQueue** Service Bus kuyruğundaki iletileri cihaz uygulamanız tarafından gönderilen Merhaba kritik iletileri çıkarır. Bu sıra ekli toohello IOT hub ' dir.

> [!NOTE]
> IOT hub'ı birçok cihaz platformları ve C, Java ve JavaScript gibi diller için SDK desteğe sahiptir. toolearn Bu öğreticide bir fiziksel cihaz ile sanal cihaz tooreplace hello nasıl hello bkz [Azure IOT Geliştirme Merkezi].

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Etkin bir Azure hesabı. <br/>Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.

Bazı temel bilgiye sahip [Azure Storage] ve [Azure Service Bus].

## <a name="send-interactive-messages"></a>Etkileşimli iletileri gönder

Hello oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile çalışmaya başlama] öğretici toooccasionally etkileşimli ileti gönderme.

Visual Studio'da, hello **SimulatedDevice** proje, hello yerine `SendDeviceToCloudMessagesAsync` koddan hello yöntemiyle:

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

Bu yöntem rastgele hello özelliği ekler `"level": "critical"` hello çözüm arka uç tarafından Acil eylem gerektiren bir ileti taklit eden bir hello aygıt tarafından gönderilen toomessages. Bu IOT hub'ın hello ileti toohello uygun mesajı hedef yönlendirebilir şekilde hello cihaz uygulaması bu bilgileri hello ileti özelliklerinde yerine hello ileti gövdesinde geçirir.

> [!NOTE]
> Özellikler tooroute ileti işleme, ayrıca burada gösterilen toohello hot yolu örnek soğuk yolu da dahil olmak üzere çeşitli senaryolar için kullanabilirsiniz.

> [!NOTE]
> Basitlik Hello artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda hello MSDN makalesinde önerilen üstel geri alma gibi bir yeniden deneme ilkesi uygulamalıdır [geçici hata işleme].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>IOT hub'ınızdaki rota iletileri tooa sırası

Bu bölümde şunları yapacaksınız:

* Service Bus kuyruğuna oluşturun.
* Tooyour IOT hub bağlayın.
* Bir özellik selamlama iletisine hello varlığını temel IOT hub toosend iletileri toohello sıranız yapılandırın.

Service Bus sıralarından tooprocess nasıl iletileri hakkında daha fazla bilgi için bkz: [kuyruklarla çalışmaya başlama][Service Bus queue].

1. Service Bus kuyruğuna açıklandığı gibi oluşturmak [kuyruklarla çalışmaya başlama][Service Bus queue]. Merhaba sıra hello olmalıdır aynı abonelikte ve bölgede IOT hub'ınızı. Merhaba ad alanı ve sıra adını not edin.

    > [!NOTE]
    > Service Bus kuyrukları ve konularından IOT Hub uç noktaları değil olarak kullanılan **oturumları** veya **yinelenen saptama** etkin. Bu seçeneklerden birini etkinleştirilirse hello uç noktası olarak görünür **ulaşılamıyor** hello Azure Portalı'nda.

2. Azure portal Merhaba, IOT hub'ınızı açın ve'ı tıklatın **uç noktaları**.
    
    ![IOT hub uç noktaları][30]

3. Merhaba, **uç noktaları** dikey penceresinde tıklatın **Ekle** en üst tooadd sıra tooyour IOT hub'ınızı hello. Ad hello endpoint **CriticalQueue** ve hello aşağı açılan listeler tooselect kullanmak **Service Bus kuyruğuna**, hizmet veri yolu ad alanı, sıra içinde bulunduğu hello ve Merhaba, kuyruk adı. İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.
    
    ![Bir uç nokta ekleme][31]
    
4. Şimdi **yollar** IOT hub'ınızdaki. Tıklatın **Ekle** hello üstünde hello dikey toocreate toohello sıra, yalnızca iletileri yönlendiren bir yönlendirme kuralı eklendi. Seçin **DeviceTelemetry** hello veri kaynağı olarak. Girin `level="critical"` hello koşulu olarak ve hello sıra yeni eklenen kural endpoint yönlendirme hello olarak özel bir uç noktası olarak seçin. İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.
    
    ![Bir yol ekleme][32]
    
    Merhaba geri dönüş rota çok ayarlandığından emin olun**ON**. Bu değer hello için varsayılan bir IOT hub yapılandırmadır.
    
    ![Geri dönüş yolu][33]

## <a name="read-from-hello-queue-endpoint"></a>Merhaba sıra uç noktasından okumak

Bu bölümde, hello sıra uç noktasından Merhaba iletileri okuyun.

1. Visual Studio'da bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme, hello kullanarak ekleyin **konsol uygulaması (.NET Framework)** proje şablonu. Ad hello proje **ReadCriticalQueue**.

2. Çözüm Gezgini'nde hello sağ **ReadCriticalQueue** proje ve ardından **NuGet paketlerini Yönet**. Bu işlem hello görüntüler **NuGet Paket Yöneticisi** penceresi.

3. Arama **WindowsAzure.ServiceBus**, tıklatın **yüklemek**ve hello kullanım koşullarını kabul edin. Bu işlem indirir, yükler ve başvuru toohello Azure Service Bus, tüm bağımlılıklarıyla birlikte ekler.

4. Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri hello hello üstündeki **Program.cs** dosyası:
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi. Yedek hello bağlantı dizesiyle **dinleme** hello sırası izinlerini:
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Visual Studio'da, Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve seçin **başlangıç projelerini Ayarla**. Seçin **birden fazla başlangıç projesi**seçeneğini belirleyip **Başlat** hello hello eylem olarak **ReadDeviceToCloudMessages**, **SimulatedDevice**, ve **ReadCriticalQueue** projeleri.
2. Tuşuna **F5** toostart hello üç konsol uygulamaları. Merhaba **ReadDeviceToCloudMessages** uygulama sahip yalnızca hello gönderilen kritik olmayan iletiler **SimulatedDevice** uygulama ve hello **ReadCriticalQueue** uygulama sahip yalnızca Kritik iletileri.
   
   ![Üç konsol uygulamaları][50]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl tooreliably gönderme cihaz bulut iletilerini IOT Hub'ının hello ileti yönlendirme işlevini kullanarak öğrendiniz.

Merhaba [toosend bulut-cihaz IOT Hub ile nasıl iletileri] [ lnk-c2d] nasıl toosend çözüm arka ucunuz tooyour aygıtlardan iletileri gösterir.

IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi][lnk-suite].

IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].

IOT Hub içinde ileti yönlendirme hakkında daha fazla toolearn bkz [IOT Hub ile iletileri almasına ve göndermesine][lnk-devguide-messaging].

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[IOT Hub ile çalışmaya başlama]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IOT Geliştirme Merkezi]: https://azure.microsoft.com/develop/iot
[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
