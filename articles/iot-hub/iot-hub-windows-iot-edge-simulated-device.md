---
title: "Azure IOT kenar (Windows) aygıtıyla aaaSimulate | Microsoft Docs"
description: "Nasıl toouse Azure IOT kenar Windows toocreate sanal bir cihaz üzerinde bir Azure IOT sınır ağ geçidi tooan IOT hub'ı aracılığıyla telemetri gönderir."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a>Bir sanal cihaz (Windows) ile Azure IOT kenar toosend cihaz bulut iletilerini kullanın

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Nasıl toorun hello örnek

Merhaba **build.cmd** betik hello çıktısını oluşturur **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu. Bu çıktı, bu örnekte kullanılan hello dört IOT kenar modüller içerir.

Merhaba yapı betik basamak:

* **Logger.dll** hello içinde **yapı\\modülleri\\Günlükçü\\hata ayıklama** klasör.
* **iothub.dll** hello içinde **yapı\\modülleri\\ıothub\\hata ayıklama** klasör.
* **kimlik\_map.dll** hello içinde **yapı\\modülleri\\identitymap\\hata ayıklama** klasör.
* **Benzetimli\_device.dll** hello içinde **yapı\\modülleri\\benzetimli\_aygıt\\hata ayıklama** klasör.

Bu yolları Merhaba kullanma **modül yolu** değerleri aşağıdaki JSON ayarları dosyasına hello gösterildiği gibi:

Benzetimli hello\_aygıt\_bulut\_karşıya\_örnek işlemi hello yol tooa JSON yapılandırma dosyası komut satırı bağımsız değişkeni olarak alır. Merhaba aşağıdaki örnek JSON dosyası hello SDK deposu sırasında sağlanan **örnekleri\\benzetimli\_aygıt\_bulut\_karşıya\_örnek\\src\\ Benzetimli\_aygıt\_bulut\_karşıya\_örnek\_win.json**. Merhaba değiştirmediğiniz sürece olduğundan bu yapılandırma dosyası works betik tooplace hello IOT kenar modülleri oluşturabilir veya yürütülebilir dosyalar varsayılan olmayan konumlarda örnek.

> [!NOTE]
> Merhaba modülü burada hello benzetimli göreli toohello dizin yollardır\_aygıt\_bulut\_karşıya\_sample.exe bulunduğu. Merhaba örnek JSON yapılandırma dosyası varsayılan olarak toowriting too'deviceCloudUploadGatewaylog.log', geçerli çalışma dizininde.

Merhaba dosyasını bir metin düzenleyicisinde açın **örnekleri\\benzetimli\_aygıt\_bulut\_karşıya\_örnek\\src\\benzetimli\_aygıt \_bulut\_karşıya\_win.json** hello yerel kopyasını içinde **IOT kenar** deposu. Bu dosya hello IOT kenar modüllerini hello örnek ağ geçidi yapılandırır:

* Merhaba **Iothub** modülü tooyour IOT hub'ı bağlar. Bu toosend veri tooyour IOT hub'ı yapılandırın. Özellikle, kümesi hello **IoTHubName** değer toohello adı IOT hub'ınızın ve ayarlayın hello **IoTHubSuffix** çok değer**azure devices.net**. Set hello **aktarım** , değer tooone: **HTTP**, **AMQP**, veya **MQTT**. Şu anda yalnızca **HTTP** tüm aygıt iletiler için bir TCP bağlantısı paylaşır. Merhaba değeri çok ayarlarsanız**AMQP**, veya **MQTT**, hello ağ geçidi bir ayrı TCP bağlantısı tooIoT Hub her aygıt için korur.
* Merhaba **eşleme** modülü sanal cihazlar tooyour IOT Hub cihaz kimliklerinizi hello MAC adreslerini eşler. Olduğundan emin olun **DeviceID** değerleri Eşleştir hello kimliklerini hello tooyour IOT hub ve o hello eklediğiniz iki aygıtları **deviceKey** değerleri içeren iki aygıtlarınızın hello anahtarları.
* Merhaba **BLE1** ve **BLE2** modüllerdir benzetimli hello aygıtlar. Nasıl hello modülü MAC adresleri hello hello eşleşen Not **eşleme** modülü.
* Merhaba **Günlükçü** modülü, ağ geçidi etkinliği tooa dosyanızı günlüğe kaydeder.
* Merhaba **modül yolu** aşağıdaki örneğine hello gösterilen burada hello benzetimli göreli toohello dizin değerlerdir\_aygıt\_bulut\_karşıya\_sample.exe bulunduğu.
* Merhaba **bağlantılar** dizi hello JSON dosyasının hello altındaki bağlayan hello **BLE1** ve **BLE2** modülleri toohello **eşleme** modülü ve hello **eşleme** modülü toohello **Iothub** modülü. Ayrıca tüm iletileri hello tarafından günlüğe kaydedilen sağlar **Günlükçü** modülü.

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

Toohello yapılandırma dosyası yaptığınız Hello Değişiklikleri Kaydet.

toorun hello örneği:

1. Bir komut isteminde toohello gidin **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu.
2. Merhaba aşağıdaki komutu çalıştırın:
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. Merhaba kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] aracı hello IOT hub'ınızın aldığı toomonitor karışılama iletileri ağ geçidi. Örneğin, ıothub explorer kullanarak cihaz bulut iletilerini komutu aşağıdaki hello kullanarak izleyebilirsiniz:

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Sonraki adımlar

toogain IOT kenarı ve deneme daha gelişmiş bir anlayış bazı kod örnekleri ile ziyaret hello aşağıdaki Geliştirici öğreticiler ve kaynaklar:

* [IOT Edge fiziksel CİHAZDAN cihaz bulut iletilerini gönder][lnk-physical-device]
* [Azure IOT kenar][lnk-iot-edge]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [IOT çözümünüzden plan hello güvenli][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md