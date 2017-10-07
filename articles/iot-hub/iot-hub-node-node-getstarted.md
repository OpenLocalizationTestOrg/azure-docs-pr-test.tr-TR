---
title: "aaaGet başlatılan Azure IOT Hub (düğüm) | Microsoft Docs"
description: "Nasıl tooAzure IOT Hub'ın IOT SDK'ları için Node.js kullanarak toosend cihaz-bulut iletileri öğrenin. Sanal cihazı ve hizmet uygulamaları tooregister Cihazınızı oluşturmak, iletileri gönderir ve IOT hub'ından iletileri okur."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Düğüm kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanın
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Bu öğretici Hello sonunda üç Node.js konsol uygulamaları vardır:

* **Createdeviceıdentity.js**ilişkili güvenlik anahtarı tooconnect sanal cihaz uygulamanız ve bir cihaz kimliği oluşturur.
* **ReadDeviceToCloudMessages.js**, sanal cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.
* **SimulatedDevice.js**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello MQTT protokolünü kullanarak her saniye bir telemetri iletisi gönderir.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.
> 
> 

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Node.js 0.10.x sürümü veya sonraki bir sürüm.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

IoT Hub’ınızı oluşturdunuz. Merhaba IOT Hub ana bilgisayar adı ve hello IOT Hub bağlantı dizesine toocomplete hello Bu öğreticinin geri kalanını ihtiyacınız var.

## <a name="create-a-device-identity"></a>Cihaz kimliği oluşturma
Bu bölümde, hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği oluşturan bir Node.js konsol uygulaması oluşturun. Bir aygıt tooIoT hub hello kimlik kayıt defterinde girişi olmayan yalnızca bağlayabilirsiniz. Daha fazla bilgi için bkz: Merhaba **kimlik kayıt defteri** hello bölümünü [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity]. Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri.

1. **createdeviceidentity** adlı yeni bir boş klasör oluşturun. Merhaba, **createdeviceidentity** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **createdeviceidentity** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** hizmet SDK paketi:
   
    ```
    npm install azure-iothub --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **Createdeviceıdentity.js** hello dosyasında **createdeviceidentity** klasör.
4. Merhaba aşağıdakileri ekleyin `require` hello hello başlangıç deyiminin **Createdeviceıdentity.js** dosyası:
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Aşağıdaki kodu toohello hello eklemek **Createdeviceıdentity.js** dosya ve hello yer tutucu değerini hello hello önceki bölümde oluşturduğunuz hello hub için IOT Hub bağlantı dizesi ile değiştirin: 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Aşağıdaki kod toocreate hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz tanımında hello ekleyin. Merhaba cihaz kimliği hello kimlik kayıt defterinde yoksa, bu kod bir cihaz oluşturur, aksi takdirde hello mevcut aygıt hello anahtarını döndürür:
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. **CreateDeviceIdentity.js** dosyasını kaydedin ve kapatın.
8. toorun hello **createdeviceidentity** uygulamayı, komut hello hello createdeviceidentity klasöründeki komut isteminde aşağıdaki hello yürütün:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Merhaba Not **cihaz kimliği** ve **aygıt anahtarı**. TooIoT hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda, bu değerleri daha sonra gerekir.

> [!NOTE]
> Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar. Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar. Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir. Daha fazla bilgi için bkz: Merhaba [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Cihazdan buluta iletileri alma
Bu bölümde, IoT Hub'dan cihazdan buluta iletiler okuyan bir Node.js konsol uygulaması oluşturacaksınız. IOT hub'ı kullanıma sunan bir [Event Hubs][lnk-event-hubs-overview]-uyumlu bir uç noktasını tooenable, tooread cihaz bulut iletilerini. tookeep şeyler basit, Bu öğretici, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur. Merhaba [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] öğretici gösterir, ölçekli olarak nasıl tooprocess cihaz-bulut iletileri. Merhaba [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Eğitmeni nasıl tooprocess olay hub'larından iletileri ve geçerli toohello IOT Hub ve Event Hub ile uyumlu uç noktalar hakkında daha fazla bilgi sağlar.

> [!NOTE]
> Merhaba cihaz bulut iletilerini her zaman okumak için Event Hub ile uyumlu uç nokta hello AMQP protokolünü kullanır.
> 
> 

1. **readdevicetocloudmessages** adlı boş bir klasör oluşturun. Merhaba, **readdevicetocloudmessages** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **readdevicetocloudmessages** klasörüne, komut tooinstall hello aşağıdaki hello **azure event hubs** paketi:
   
    ```
    npm install azure-event-hubs --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **ReadDeviceToCloudMessages.js** hello dosyasında **readdevicetocloudmessages** klasör.
4. Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **ReadDeviceToCloudMessages.js** dosyası:
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Değişken bildirimi aşağıdaki hello ekleyin ve hello hub'ınız için IOT Hub bağlantı dizesine sahip hello yer tutucu değerini değiştirin:
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Yazdırma çıktı toohello Konsolu iki işlevleri aşağıdaki hello ekleyin:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Aşağıdaki kod toocreate hello hello eklemek **EventHubClient**hello bağlantı tooyour IOT hub'ı açın ve her bölüm için alıcı oluşturun. Bu uygulama Hello alıcı çalışmaya başladıktan sonra hello alıcı yalnızca gönderilen iletileri tooIoT Hub okur böylece bir alıcı oluştururken bir filtre kullanır. Yalnızca hello geçerli iletiler kümesini görmek için bu filtre bir test ortamında kullanışlıdır. Bir üretim ortamında kodunuzun tüm hello iletileri işlediğinden emin olmanız gerekir. Daha fazla bilgi için bkz: Merhaba [nasıl tooprocess IOT Hub cihaz bulut iletilerini] [ lnk-process-d2c-tutorial] Öğreticisi:
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Kaydet ve Kapat hello **ReadDeviceToCloudMessages.js** dosya.

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde, tooan IOT hub'ı cihaz-bulut iletileri gönderen bir cihaza benzetim yapan bir Node.js konsol uygulaması oluşturun.

1. **simulateddevice** adlı boş bir klasör oluşturun. Merhaba, **simulateddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **simulateddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **SimulatedDevice.js** hello dosyasında **simulateddevice** klasör.
4. Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **SimulatedDevice.js** dosyası:
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği. Değiştir **{youriothostname}** hello IOT hub'ı hello adı ile oluşturduğunuz hello *IOT Hub oluşturma* bölümü. Değiştir **{yourdevicekey}** hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Merhaba uygulamadan işlevi toodisplay çıktı aşağıdaki hello ekleyin:
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Bir geri çağırma oluşturun ve hello kullan **setInterval** saniyede bir ileti tooyour IOT hub'ı toosend işlev:
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. Merhaba bağlantı tooyour IOT hub'ı açın ve iletileri göndermeye başlayın:
   
    ```
    client.open(connectCallback);
    ```
9. Kaydet ve Kapat hello **SimulatedDevice.js** dosya.

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Bir komut isteminde hello **readdevicetocloudmessages** klasörü, IOT hub'ınızı izleme komut toobegin aşağıdaki hello çalıştırın:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IOT Hub hizmeti uygulama toomonitor cihaz-bulut iletileri][7]
2. Bir komut isteminde hello **simulateddevice** klasörü, telemetri verileri tooyour IOT hub'ı gönderme komutu toobegin aşağıdaki hello çalıştırın:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IOT Hub cihaz uygulaması toosend cihaz bulut iletilerini][8]
3. Merhaba **kullanım** döşeme hello [Azure portal] [ lnk-portal] gösterir hello gönderilen iletileri toohello IOT hub'ı sayısı:
   
    ![Azure portalı kullanım kutucuğu sayısını gösteren gönderilen iletileri tooIoT Hub][43]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Bu cihaz kimliğini tooenable benzetimli hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır. Merhaba hello IOT hub tarafından alınan iletileri görüntüleyen bir uygulama da oluşturmuş. 

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

* [Cihazınızı bağlama][lnk-connect-device]
* [Cihaz yönetimini kullanmaya başlama][lnk-device-management]
* [Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]

toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
