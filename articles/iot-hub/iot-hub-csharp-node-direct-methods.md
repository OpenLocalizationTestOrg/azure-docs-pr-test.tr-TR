---
title: "Azure IOT Hub aaaUse doğrudan yöntemleri (.NET/düğümü) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub yöntemleri doğrudan. Node.js tooimplement doğrudan yöntemi ve hello .NET tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Doğrudan yöntemleri (.NET/düğüm) kullanın
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Bu öğreticide, biz toodevelop bir .NET ve bir Node.js konsol uygulaması yapacaksınız:

* **CallMethodOnDevice.sln**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüler .NET arka uç uygulaması.
* **SimulatedDevice.js**, tooyour IOT hub'ı daha önce oluşturulan hello cihaz kimliğiyle bağlanan bir cihaza benzetim ve hello bulut tarafından adlı toohello yöntemi yanıt bir Node.js uygulaması.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.
> 
> 

toocomplete Bu öğretici, gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Node.js 0.10.x sürümü veya sonraki bir sürüm.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde, hello çözüm tarafından arka uç adlı tooa yöntemi yanıt bir Node.js konsol uygulaması oluşturun.

1. **simulateddevice** adlı yeni bir boş klasör oluşturun. Merhaba, **simulateddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **simulateddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** paketler:
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak, bir dosya hello oluşturun **simulateddevice** klasörü ve adlandırın **SimulatedDevice.js**.
4. Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **SimulatedDevice.js** dosyası:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Ekleme bir **connectionString** değişken ve toocreate kullanan bir **DeviceClient** örneği. Değiştir **{cihaz bağlantı dizesi}** hello oluşturulan hello cihaz bağlantı dizesiyle *bir cihaz kimliği oluşturma* bölümü:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Merhaba aygıtta işlevi tooimplement hello doğrudan yöntemi aşağıdaki hello ekleyin:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Merhaba bağlantı tooyour IOT hub'ı açın ve hello yöntemi dinleyicisi başlatılamıyor:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Kaydet ve Kapat hello **SimulatedDevice.js** dosya.

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (bağlantı yeniden deneme), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Bir cihazda doğrudan bir yöntem çağrısı
Bu bölümde, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir .NET konsol uygulaması oluşturun.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü. Ad hello proje **CallMethodOnDevice**.
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10]
2. Çözüm Gezgini'nde hello sağ **CallMethodOnDevice** proje ve ardından **NuGet paketlerini Yönet...** .
3. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi][11]

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

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Buna Visual Studio Çözüm Gezgini Merhaba, çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** . Seçin **tek başlangıç projesi**ve ardından hello **CallMethodOnDevice** hello açılır menüsünde projesinde.

2. Bir komut isteminde hello **simulateddevice** klasörü, IOT Hub'ınızı gelen yöntem çağrıları için dinleme komutu toostart aşağıdaki hello çalıştırın:
   
    ```
    node SimulatedDevice.js
    ```
   Benzetimli hello aygıt tooopen bekler:![][7]
3. Şimdi bu hello cihaz bağlı ve hello .NET çalıştırmak için yöntem çağrılarına bekleniyor, **CallMethodOnDevice** hello sanal cihaz uygulamasının uygulama tooinvoke hello yöntemi. Merhaba konsolunda yazılmış hello aygıt yanıtı görmeniz gerekir.
   
    ![][8]
4. Hello aygıt sonra bu iletiyi yazdırma tarafından toohello yöntemi tepki verir:
   
    ![][9]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır. Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş. 

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

* [IOT Hub ile çalışmaya başlama]
* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
