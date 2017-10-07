---
title: "Azure IOT hub'ı (düğüm) aaaCloud cihaza iletileriyle | Microsoft Docs"
description: "Nasıl toosend bulut-cihaz hello Azure IOT SDK'ları için Node.js kullanarak Azure IOT hub'ı tooa aygıttan iletileri. Bir sanal cihaz uygulaması tooreceive bulut-cihaz iletilerini değiştirmek ve arka uç uygulaması toosend hello bulut-cihaz iletilerini değiştirin."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>IOT hub'ı (düğüm) sahip bulut-cihaz iletilerini gönder
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Giriş
Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir. Merhaba [IOT Hub ile çalışmaya başlama] öğretici nasıl toocreate IOT hub'ı, bir cihaz kimliği, sağlamak ve cihaz-bulut iletileri gönderen bir sanal cihaz uygulamasının kodu gösterir.

Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama]. Size bir nasıl gösterir için:

* Çözüm arka ucunuz, bulut-cihaz iletilerini tooa tek cihaz IOT hub'ı aracılığıyla gönderin.
* Bir cihazda bulut-cihaz iletilerini alır.
* Çözüm arka ucunuz, teslimat alındısı iste (*geri bildirim*) tooa cihaz IOT Hub'ından gönderilen iletileri için.

Hello bulut-cihaz iletilerini hakkında daha fazla bilgi bulabilirsiniz [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].

Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları çalıştırın:

* **SimulatedDevice**, oluşturulan hello uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama], hangi tooyour IOT hub'ı bağlar ve bulut-cihaz iletilerini alır.
* **SendCloudToDeviceMessage**, hangi bulut aygıt iletisi toohello sanal cihaz uygulaması IOT hub'ı üzerinden gönderir ve teslimat alındısı alır.

> [!NOTE]
> IOT Hub SDK desteği birçok cihaz platformları ve Azure IOT cihaz SDK'ları aracılığıyla dilleri (C, Java ve Javascript dahil) sahiptir. Adım adım yönergeler nasıl tooconnect aygıt toothis öğreticinin kod ve genellikle tooAzure IOT hub'ı görmek için hello [Azure IOT Geliştirme Merkezi].
> 
> 

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Node.js 0.10.x sürümü veya sonraki bir sürüm.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Merhaba sanal cihaz uygulamasının ileti alma
Bu bölümde, oluşturduğunuz hello sanal cihaz uygulamasının değiştirme [IOT Hub ile çalışmaya başlama] tooreceive bulut cihaza iletilerden hello IOT hub'ı.

1. Bir metin düzenleyicisi kullanarak hello SimulatedDevice.js dosyasını açın.
2. Merhaba değiştirme **connectCallback** IOT Hub'ından gönderilen toohandle iletileri işlev. Bu örnekte, hello cihaz her zaman hello çağırır **tam** toonotify IOT Hub'ın selamlama iletisine işlediğinden işlev. Yeni hello sürümünüz **connectCallback** işlevi hello parçacığını aşağıdaki gibi görünür:
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > HTTP MQTT veya AMQP yerine hello taşıma olarak kullanırsanız, hello **DeviceClient** seyrek IOT Hub (değerinden 25 dakikada bir) gelen iletileri örneği denetler. Merhaba hello farklarını MQTT, AMQP ve HTTP desteği ve IOT hub'ı azaltma hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Bulut cihaza ileti gönderme
Bu bölümde, bulut-cihaz iletilerini toohello sanal cihaz uygulamasının gönderen bir Node.js konsol uygulaması oluşturun. Hello eklediğiniz hello aygıtın aygıt kimliği hello [IOT Hub ile çalışmaya başlama] Öğreticisi. Hello bulabileceğiniz hub'ınız için IOT Hub bağlantı dizesine hello de [Azure portal].

1. Adlı bir boş klasör oluşturun **sendcloudtodevicemessage**. Merhaba, **sendcloudtodevicemessage** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```shell
    npm init
    ```
2. Merhaba, komut isteminde **sendcloudtodevicemessage** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** paketi:
   
    ```shell
    npm install azure-iothub --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **SendCloudToDeviceMessage.js** hello dosyasında **sendcloudtodevicemessage** klasör.
4. Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **SendCloudToDeviceMessage.js** dosyası:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Kod çok aşağıdaki hello eklemek**SendCloudToDeviceMessage.js** dosya. "{IOT hub bağlantı dizesine}" Merhaba yer tutucu değerini hello hello oluşturduğunuz hello hub için IOT Hub bağlantı dizesi ile değiştirin [IOT Hub ile çalışmaya başlama] Öğreticisi. "{Aygıt id}" Merhaba yer tutucu hello aygıt hello eklediğiniz hello aygıtın Kimliğini değiştirin [IOT Hub ile çalışmaya başlama] Öğreticisi:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. İşlev tooprint işlemi sonuçları toohello Konsolu aşağıdaki hello ekleyin:
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. İşlev tooprint teslim geri bildirim iletileri toohello Konsolu aşağıdaki hello ekleyin:
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Merhaba aşağıdaki toosend bir ileti tooyour aygıt kod ve hello aygıt hello bulut cihaz iletiyi onayladıktan zaman hello geri bildirim iletisi işlemek ekleyin:
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. Kaydet ve Kapat **SendCloudToDeviceMessage.js** dosya.

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba hello komut isteminde **simulateddevice** klasörü hello aşağıdaki komutu çalıştırın, komut toosend telemetri tooIoT Hub ve bulut-cihaz iletilerini toolisten:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Merhaba sanal cihaz uygulamasının çalıştırın][img-simulated-device]
2. Bir komut isteminde hello **sendcloudtodevicemessage** klasörü, bir bulut cihaz ileti komutu toosend aşağıdaki hello çalıştırın ve hello bildirim geri bildirim için bekleyin:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Merhaba uygulama toosend hello bulut cihaz komutunu çalıştırın][img-send-command]
   
   > [!NOTE]
   > Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].
   > 
   > 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl öğrenilen toosend ve bulut-cihaz iletilerini. 

IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi].

IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[Azure IoT Geliştirici Merkezi]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[Geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IoT Paketi]: https://azure.microsoft.com/documentation/suites/iot-suite/
