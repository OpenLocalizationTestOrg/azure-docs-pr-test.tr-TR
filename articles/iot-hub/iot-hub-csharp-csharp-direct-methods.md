---
title: "Azure IOT Hub aaaUse doğrudan yöntemleri (.NET/.NET) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub yöntemleri doğrudan. .NET tooimplement doğrudan yöntemi ve hello .NET tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Doğrudan yöntemleri (.NET/.NET) kullanın
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Bu öğreticide, devam eden toodevelop iki .NET konsol uygulamaları şunlardır:

* **CallMethodOnDevice**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüler bir arka uç uygulaması.
* **SimulateDeviceMethods**, tooyour IOT hub'ı daha önce oluşturulan hello cihaz kimliğiyle bağlanan bir cihaza benzetim ve hello bulut tarafından adlı toohello yöntemi yanıt bir konsol uygulaması.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.
> 
> 

toocomplete Bu öğretici, gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Toocreate hello cihaz kimliği programlı olarak bunun yerine isterseniz, hello hello ilgili bölümünü okuyun [.NET kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanmak] [ lnk-device-identity-csharp] makalesi.


## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde, hello çözüm tarafından arka uç adlı tooa yöntemi yanıt veren bir .NET konsol uygulaması oluşturun.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Ad hello proje **SimulateDeviceMethods**.
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]
    
1. Çözüm Gezgini'nde hello sağ **SimulateDeviceMethods** proje ve ardından **NuGet paketlerini Yönet...** .
1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**. Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba yer tutucu değerini hello önceki bölümünde belirtildiği hello cihaz bağlantı dizesini değiştirin.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Merhaba aygıtta tooimplement hello doğrudan yöntemi aşağıdaki hello ekleyin:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Son olarak, aşağıdaki kod toohello hello eklemek **ana** yöntemi tooopen hello bağlantı tooyour IOT hub ve başlatma hello yöntemi dinleyicisi:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. Buna Visual Studio Çözüm Gezgini Merhaba, çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** . Seçin **tek başlangıç projesi**ve ardından hello **SimulateDeviceMethods** hello açılır menüsünde projesinde.        

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (bağlantı yeniden deneme), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Bir cihazda doğrudan bir yöntem çağrısı
Bu bölümde, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir .NET konsol uygulaması oluşturun.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü. Ad hello proje **CallMethodOnDevice**.
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createserviceapp]
2. Çözüm Gezgini'nde hello sağ **CallMethodOnDevice** proje ve ardından **NuGet paketlerini Yönet...** .
3. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]

4. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Bu yöntem adı ile doğrudan bir yöntem çağırır `writeLine` hello üzerinde `myDeviceId` aygıt. Ardından, hello konsolunda hello aygıt tarafından sağlanan hello yanıt yazar. Nasıl olası toospecify hello aygıt toorespond için zaman aşımı değeri olduğuna dikkat edin.
7. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Buna Visual Studio Çözüm Gezgini Merhaba, çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** . Seçin **tek başlangıç projesi**ve ardından hello **CallMethodOnDevice** hello açılır menüsünde projesinde.

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba .NET cihaz uygulamayı çalıştırma **SimulateDeviceMethods**. IOT Hub'ınızı gelen yöntem çağrıları için dinleme başlamanız gerekir: 

    ![Cihaz uygulaması çalıştırın][img-deviceapprun]
1. Şimdi bu hello cihaz bağlı ve hello .NET çalıştırmak için yöntem çağrılarına bekleniyor, **CallMethodOnDevice** hello sanal cihaz uygulamasının uygulama tooinvoke hello yöntemi. Merhaba konsolunda yazılmış hello aygıt yanıtı görmeniz gerekir.
   
    ![Hizmet uygulaması çalıştırın][img-serviceapprun]
1. Hello aygıt sonra bu iletiyi yazdırma tarafından toohello yöntemi tepki verir:
   
    ![Merhaba aygıtta çağrılan doğrudan yöntemi][img-directmethodinvoked]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır. Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş. 

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

* [IOT Hub ile çalışmaya başlama]
* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
