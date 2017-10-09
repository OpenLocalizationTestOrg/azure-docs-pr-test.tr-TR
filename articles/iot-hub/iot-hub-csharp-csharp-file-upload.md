---
title: "aygıtları tooAzure IOT Hub .NET ile aaaUpload dosyalarından | Microsoft Docs"
description: ".NET için Azure IOT cihaz SDK'sını kullanarak bir aygıtı toohello buluttan nasıl tooupload dosyaları. Karşıya yüklenen dosyaların bir Azure depolama blob kapsayıcısında depolanır."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>.NET kullanarak IOT Hub ile cihaz toohello bulut dosyaları karşıya yükleme

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Bu öğretici hello hello kodda inşa edilmiştir [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) öğretici tooshow, nasıl toouse hello IOT Hub'ın dosya karşıya yükleme özellikleri. Size bir nasıl gösterir için:

- Güvenli bir şekilde bir aygıt ile Azure sağlayan bir dosya yüklemek için URI blob.
- Merhaba, uygulama arka ucu IOT hub'ı dosya karşıya yükleme bildirimleri tootrigger işleme hello dosyasında kullanın.

Merhaba [IOT Hub ile çalışmaya başlama](iot-hub-csharp-csharp-getstarted.md) ve [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) öğreticiler hello temel cihaz Bulut ve bulut-cihaz Mesajlaşma işlevlerini IOT hub'ı gösterir. Merhaba [işlem cihaz-bulut iletileri](iot-hub-csharp-csharp-process-d2c.md) öğretici bir şekilde tooreliably store cihaz bulut iletilerini Azure blob depolama alanındaki açıklar. Ancak, bazı senaryolarda hello veri cihazlarınızı IOT hub'ı kabul eden hello görece küçük cihaz bulut iletilere Gönder kolayca eşlenemiyor. Örneğin:

* Görüntüleri içeren büyük dosyaları
* Videolar
* Yüksek sıklıkta örneklenen titreşimi veri
* Önceden işlenmiş veri çeşit

Bu dosyalar genellikle gibi araçları kullanılarak hello bulutta işlenen toplu olan [Azure Data Factory](../data-factory/index.md) veya hello [Hadoop](../hdinsight/index.md) yığını. Bir aygıt tooupload dosyalarından gerektiğinde, hello güvenliği ve güvenilirliği için IOT hub'ı kullanmaya devam edebilirsiniz.

Merhaba Bu öğreticinin sonunda iki .NET konsol uygulamaları çalıştırın:

* **SimulatedDevice**, hello oluşturulan hello uygulaması değiştirilmiş bir sürümünü [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) Öğreticisi. Bu uygulama, IOT hub tarafından sağlanan bir SAS URI'sini kullanarak bir dosya toostorage yükler.
* **ReadFileUploadNotification**, IOT hub'ından dosya karşıya yükleme bildirimlerini alır.

> [!NOTE]
> IOT hub'ı Azure IOT cihaz SDK'ları çok sayıda cihaz platformları ve (C, Java ve Javascript gibi) dilleri destekler. Toohello başvuran [Azure IOT Geliştirme Merkezi] hakkında adım adım yönergeler için tooconnect, IOT Hub cihaz tooAzure.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Bir aygıt uygulamasından bir dosyayı karşıya yüklemek

Bu bölümde, oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) tooreceive bulut cihaza iletilerden hello IOT hub'ı.

1. Visual Studio'da hello sağ **SimulatedDevice** proje, tıklatın **Ekle**ve ardından **varolan öğeyi**. Tooan görüntü dosyasına gidin ve projenize ekleyin. Bu öğretici hello görüntü adlandırılan varsayar `image.jpg`.

1. Merhaba görüntüde sağ tıklayın ve ardından **özellikleri**. Olduğundan emin olun **tooOutput dizin kopyalama** çok ayarlanır**her zaman Kopyala**.

    ![][1]

1. Merhaba, **Program.cs** dosya, aşağıdaki deyimleri hello dosyanın üst kısmındaki hello hello ekleyin:

    ```csharp
    using System.IO;
    ```

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Merhaba `UploadToBlobAsync` yöntemi hello dosya adını alır ve hello dosya toobe akış kaynağı karşıya ve hello karşıya yükleme toostorage işler. Merhaba konsol uygulaması hello süresini tooupload hello dosya görüntüler.

1. Merhaba yönteminde aşağıdaki hello eklemek **ana** hello önceki yöntemi `Console.ReadLine()` satır:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].

## <a name="receive-a-file-upload-notification"></a>Dosya karşıya yükleme bildirimi

Bu bölümde IOT hub'dan dosya karşıya yükleme bildirim iletileri alan bir .NET konsol uygulaması yazma.

1. Merhaba geçerli Visual Studio çözümünde hello kullanarak bir Visual C# Windows projesi oluşturma **konsol uygulaması** proje şablonu. Ad hello proje **ReadFileUploadNotification**.

    ![Visual Studio'da yeni proje][2]

1. Çözüm Gezgini'nde hello sağ **ReadFileUploadNotification** proje ve ardından **NuGet paketlerini Yönet...** .

1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, arama **Microsoft.Azure.Devices**, tıklatın **yüklemek**ve hello kullanım koşullarını kabul edin.

    Bu eylem indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sı NuGet paketi] hello içinde **ReadFileUploadNotification** projesi.

1. Merhaba, **Program.cs** dosya, aşağıdaki deyimleri hello dosyanın üst kısmındaki hello hello ekleyin:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Yedek hello IOT hub bağlantı dizesinden ile Merhaba yer tutucu değerini [IOT Hub ile çalışmaya başlama]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Bu alma düzeni aynı bir kullanılan tooreceive bulut-cihaz iletilerini hello aygıt uygulamadan hello unutmayın.

1. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello uygulamaları sunulmuştur.

1. Visual Studio'da Çözümünüze sağ tıklayın ve seçin **başlangıç projelerini Ayarla**. Seçin **birden fazla başlangıç projesi**seçeneğini belirleyip hello **Başlat** eylemi için **ReadFileUploadNotification** ve **SimulatedDevice**.

1. Tuşuna **F5**. Her iki uygulamayı başlamanız gerekir. Bir konsol uygulamasında hello karşıya yükleme tamamlandı ve diğer konsol uygulaması tarafından alınan hello karşıya yükleme bildirim iletisi hello görmeniz gerekir. Merhaba kullanabilirsiniz [Azure portal] veya hello hello varlığını için Visual Studio Sunucu Gezgini toocheck karşıya dosya Azure depolama hesabınızdaki.

    ![][50]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, nasıl toouse hello dosyayı karşıya IOT Hub'ın cihazlardan toosimplify dosya yüklemeleri yeteneklerini öğrendiniz. Aşağıdaki makaleleri hello ile tooexplore IOT hub özellikleri ve senaryoları devam edebilirsiniz:

* [IOT hub'ı program aracılığıyla oluşturma][lnk-create-hub]
* [Giriş tooC SDK][lnk-c-sdk]
* [Azure IOT SDK'ları][lnk-sdks]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[Azure portal]: https://portal.azure.com/

[Azure IOT Geliştirme Merkezi]: http://www.azure.com/develop/iot

[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure IOT hizmeti SDK'sı NuGet paketi]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
