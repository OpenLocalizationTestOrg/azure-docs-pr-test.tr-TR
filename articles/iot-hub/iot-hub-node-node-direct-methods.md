---
title: "aaaAzure IOT hub'ı doğrudan yöntemleri (düğüm) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub yöntemleri doğrudan. Doğrudan bir yöntem içeren bir sanal cihaz uygulamasının ve hello doğrudan yöntemini çağıran bir hizmet uygulaması için Node.js tooimplement hello Azure IOT SDK'ları kullanın."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>IOT cihazınızla Node.js doğrudan yöntemleri kullan
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:

* **CallMethodOnDevice.js**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüler.
* **SimulatedDevice.js**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello bulut tarafından adlı toohello yöntemi yanıt verir.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.
> 
> 

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Node.js 0.10.x sürümü veya sonraki bir sürüm.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde, hello bulut tarafından adlı tooa yöntemi yanıt bir Node.js konsol uygulaması oluşturun.

1. **simulateddevice** adlı yeni bir boş klasör oluşturun. Merhaba, **simulateddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **simulateddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SimulatedDevice.js** hello dosyasında **simulateddevice** klasör.
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
6. Merhaba aygıtta işlevi tooimplement hello yöntemi aşağıdaki hello ekleyin:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Merhaba bağlantı tooyour IOT hub'ı açın ve başlatma hello yöntemi dinleyicisini başlatmak:
   
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

## <a name="call-a-method-on-a-device"></a>Bir cihazda bir yöntemini çağırın
Bu bölümde, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir Node.js konsol uygulaması oluşturun.

1. Adlı yeni bir boş klasör oluşturun **callmethodondevice**. Merhaba, **callmethodondevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **callmethodondevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** paketi:
   
    ```
    npm install azure-iothub --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **CallMethodOnDevice.js** hello dosyasında **callmethodondevice** klasör.
4. Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **CallMethodOnDevice.js** dosyası:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Değişken bildirimi aşağıdaki hello ekleyin ve hello hub'ınız için IOT Hub bağlantı dizesine sahip hello yer tutucu değerini değiştirin:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Merhaba istemci tooopen hello bağlantı tooyour IOT hub'ı oluşturun.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. İşlevi tooinvoke hello aygıt yöntemi ve yazdırma hello aygıt yanıt toohello Konsolu aşağıdaki hello ekleyin:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Kaydet ve Kapat hello **CallMethodOnDevice.js** dosya.

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Bir komut isteminde hello **simulateddevice** klasörü, IOT Hub'ınızı gelen yöntem çağrıları için dinleme komutu toostart aşağıdaki hello çalıştırın:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. Bir komut isteminde hello **callmethodondevice** klasörü, IOT hub'ınızı izleme komut toobegin aşağıdaki hello çalıştırın:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Merhaba aygıt selamlama iletisine ve hello aygıttan hello yöntemi görüntü hello yanıt olarak adlandırılan Merhaba uygulaması yazdırma tarafından toohello yöntemi tepki görürsünüz:
   
    ![][9]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır. Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş. 

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

* [IOT Hub ile çalışmaya başlama]
* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
