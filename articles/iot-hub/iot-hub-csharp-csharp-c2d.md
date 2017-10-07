---
title: "aaaCloud aygıt iletileri ile Azure IOT hub'ı (.NET) | Microsoft Docs"
description: "Nasıl toosend bulut-cihaz hello Azure IOT SDK'ları için .NET kullanarak Azure IOT hub'ı tooa aygıttan iletileri. Bir aygıt uygulama tooreceive bulut-cihaz iletilerini değiştirmek ve bir arka uç uygulaması toosend hello bulut-cihaz iletilerini değiştirin."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>İletileri hello bulut tooyour cihaz IOT hub'ı (.NET) ile gönderin.
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Giriş
Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir. Merhaba [IOT Hub ile çalışmaya başlama] öğretici nasıl toocreate IOT hub'ı, bir cihaz kimliği, sağlamak ve cihaz-bulut iletileri gönderen bir aygıt uygulama kodu gösterir.

Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama]. Size bir nasıl gösterir için:

* Çözüm arka ucunuz, bulut-cihaz iletilerini tooa tek cihaz IOT hub'ı aracılığıyla gönderin.
* Bir cihazda bulut-cihaz iletilerini alır.
* Çözüm arka ucunuz, teslimat alındısı iste (*geri bildirim*) tooa cihaz IOT Hub'ından gönderilen iletileri için.

Hello bulut-cihaz iletilerini hakkında daha fazla bilgi bulabilirsiniz [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].

Bu öğreticinin Hello sonunda, iki .NET konsol uygulamaları çalıştırın:

* **SimulatedDevice**, oluşturulan hello uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama], hangi tooyour IOT hub'ı bağlar ve bulut-cihaz iletilerini alır.
* **SendCloudToDevice**, hangi bulut aygıt iletisi toohello cihaz uygulaması IOT hub'ı üzerinden gönderir ve teslimat alındısı alır.

> [!NOTE]
> IOT hub'ı aracılığıyla birçok cihaz platformları ve (C, Java ve Javascript dahil) dillerin SDK desteği olan [Azure IOT cihaz SDK'ları]. Adım adım yönergeler nasıl tooconnect aygıt toothis öğreticinin kod ve genellikle tooAzure IOT hub'ı görmek için hello [IOT Hub Geliştirici Kılavuzu].
> 
> 

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

## <a name="receive-messages-in-hello-device-app"></a>Merhaba aygıt uygulamada ileti alma
Bu bölümde, oluşturduğunuz hello cihaz uygulaması değiştireceksiniz [IOT Hub ile çalışmaya başlama] tooreceive bulut cihaza iletilerden hello IOT hub'ı.

1. Visual Studio'da, hello **SimulatedDevice** projesi, yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    Merhaba `ReceiveAsync` yöntemi zaman uyumsuz olarak döndürür alınan selamlama iletisine hello aygıt tarafından alınan hello zaman. Döndürdüğü *null* specifiable zaman aşımı süresinden sonra (Bu durumda, bir dakika hello varsayılan kullanılır). Merhaba uygulama zaman alan bir *null*, yeni iletiler için toowait devam etmelidir. Bu gereksinim hello hello nedeni `if (receivedMessage == null) continue` satır.
   
    Çağrı çok hello`CompleteAsync()` IOT Hub, selamlama iletisine başarıyla işlendiğinden bildirir. Merhaba ileti güvenli bir şekilde hello aygıt sıradan kaldırılabilir. Bir şey selamlama iletisine hello işlenmesini tamamlanmasını o önlenmiş hello cihaz uygulaması oluştuysa, IOT Hub tarafından tekrar teslim edilir. Ardından hello cihaz uygulama mantığını işleme o iletisi önemli *ıdempotent*, aynı iletiyi birden çok kez üreten hello alma hello aynı sonucu. Bir uygulama geçici olarak IOT hub'ı gelecekteki tüketimi için hello sırasındaki selamlama iletisine koruma sonuçları bir ileti iptal. Veya Merhaba uygulaması kalıcı olarak selamlama iletisine hello kuyruktan kaldırır bir ileti reddedebilirsiniz. Merhaba hello bulut cihaz ileti yaşam döngüsü hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > HTTP MQTT veya AMQP yerine bir taşıma olarak kullanırken, hello `ReceiveAsync` yöntemi hemen döndürür. desteklenen hello düzeni için HTTP ile bulut-cihaz iletilerini denetleyen aralıklı bağlı seyrek iletileri (değerinden 25 dakikada bir) cihazlar içindir. Daha fazla HTTP veren sonuçları IOT hub'ı azaltma hello isteklerini alır. Merhaba hello farklarını MQTT, AMQP ve HTTP desteği ve IOT hub'ı azaltma hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].
   > 
   > 
2. Merhaba yönteminde aşağıdaki hello eklemek **ana** hello önceki yöntemi `Console.ReadLine()` satır:
   
        ReceiveC2dAsync();

> [!NOTE]
> Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Bulut cihaza ileti gönderme
Bu bölümde, bulut-cihaz iletilerini toohello cihaz uygulaması gönderir bir .NET konsol uygulaması yazma.

1. Merhaba geçerli Visual Studio çözümünde hello kullanarak bir Visual C# masaüstü uygulaması projesi oluşturma **konsol uygulaması** proje şablonu. Ad hello proje **SendCloudToDevice**.
   
    ![Visual Studio'da yeni proje][20]
2. Çözüm Gezgini'nde, hello çözüme sağ tıklayın ve ardından **çözüm için NuGet paketlerini Yönet...** . 
   
    Bu eylemin hello açılır **NuGet paketlerini Yönet** penceresi.
3. Arama **Microsoft.Azure.Devices**, tıklatın **yüklemek**ve hello kullanım koşullarını kabul edin. 
   
    Bu indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sı NuGet paketi].

4. Merhaba aşağıdakileri ekleyin `using` deyimi hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices;
5. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Yedek hello yer tutucu değerini hello IOT hub bağlantı dizesinden ile [IOT Hub ile çalışmaya başlama]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Bu yöntem, yeni bir bulut aygıt iletisi toohello aygıt hello kimlikli gönderir `myFirstDevice`. Bu parametre yalnızca bir kullanılan hello gelen değişiklik tıklarsanız [IOT Hub ile çalışmaya başlama].
7. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. Visual Studio'dan Çözümünüze sağ tıklayın ve seçin **başlangıç projelerini Ayarla...** . Seçin **birden fazla başlangıç projesi**seçeneğini belirleyip hello **Başlat** eylemi için **ReadDeviceToCloudMessages**, **SimulatedDevice**, ve **SendCloudToDevice**.
9. Tuşuna **F5**. Üç uygulama başlamanız gerekir. Select hello **SendCloudToDevice** windows ve tuşuna **Enter**. Merhaba cihaz uygulaması tarafından alınan hello iletiyi görmeniz gerekir.
   
   ![Uygulama alma iletisi][21]

## <a name="receive-delivery-feedback"></a>Teslim geri alma
Bu, olası toorequest teslim (veya sona erme) IOT hub'dan ilişkin bildirimleri her bulut cihaz ileti olur. Bu seçeneği etkinleştirir hello çözüm arka ucu tooeasily Yeniden Dene'yi tıklatın veya maaş mantığı bildirin. Merhaba bulut cihaz geri bildirim hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].

Bu bölümde, hello değiştirme **SendCloudToDevice** uygulama toorequest geri bildirim ve IOT Hub'ından alırsınız.

1. Visual Studio'da, hello **SendCloudToDevice** projesi, yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    Bu alma düzeni aynı bir kullanılan tooreceive bulut-cihaz iletilerini hello aygıt uygulamadan hello unutmayın.
2. Merhaba yönteminde aşağıdaki hello eklemek **ana** hello hemen sonra yöntemi `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` satır:
   
        ReceiveFeedbackAsync();
3. toorequest geribildirim bulut cihaz iletinizin hello teslimi için toospecify bir özelliğe sahip hello **SendCloudToDeviceMessageAsync** yöntemi. Satır, hemen sonra hello aşağıdaki hello eklemek `var commandMessage = new Message(...);` satır:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Basarak Hello uygulamaları çalıştırmak **F5**. Başlangıç üç uygulama görmeniz gerekir. Select hello **SendCloudToDevice** windows ve tuşuna **Enter**. İleti hello cihaz uygulaması tarafından ve birkaç saniye sonra alınan, hello tarafından alınan geri bildirim iletisi hello görmeniz gerekir, **SendCloudToDevice** uygulama.
   
   ![Uygulama alma iletisi][22]

> [!NOTE]
> Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl öğrenilen toosend ve bulut-cihaz iletilerini. 

IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi].

IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IOT hizmeti SDK'sı NuGet paketi]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[IOT Hub ile çalışmaya başlama]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IOT paketi]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Azure IOT cihaz SDK'ları]: iot-hub-devguide-sdks.md