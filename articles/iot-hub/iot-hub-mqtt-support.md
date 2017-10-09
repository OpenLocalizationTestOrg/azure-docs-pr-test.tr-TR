---
title: Azure IOT Hub MQTT destek aaaUnderstand | Microsoft Docs
description: "Geliştirici Kılavuzu - IOT Hub cihaz dönük kullanan uç noktasını tooan bağlanan cihazları MQTT Protokolü hello desteği. Hello Azure IOT cihaz SDK'ları yerleşik MQTT desteği hakkında bilgi içerir."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Merhaba MQTT protokolünü kullanarak, IOT hub ile iletişim

IOT hub'ı etkinleştirir aygıtları toocommunicate hello IOT Hub cihaz uç hello kullanarak ile [MQTT v3.1.1] [ lnk-mqtt-org] 8883 bağlantı noktası veya bağlantı noktası 443 üzerinden WebSocket protokolü üzerinden MQTT v3.1.1 protokolü. IOT hub'ı TLS/SSL kullanılarak güvenlik altına tüm cihaz iletişimi toobe gerektirir (Bu nedenle, IOT hub'ı güvenli olmayan bağlantıları 1883 bağlantı noktası üzerinden olarak desteklemiyor).

## <a name="connecting-tooiot-hub"></a>TooIoT Hub bağlanma

Bir cihazı hello hello kitaplıklarında kullanarak ya da hello MQTT Protokolü tooconnect tooan IOT hub'ı kullanmak [Azure IOT SDK'ları] [ lnk-device-sdks] veya doğrudan hello MQTT protokolünü kullanarak.

## <a name="using-hello-device-sdks"></a>Merhaba cihaz SDK'ları kullanma

[Cihaz SDK'ları] [ lnk-device-sdks] Bu destek hello MQTT Protokolü Java, Node.js, C, C# ve Python için kullanılabilir. Merhaba cihaz SDK'ları hello standart IOT Hub bağlantı dizesi tooestablish bir bağlantı tooan IOT hub'ı kullanın. toouse hello MQTT Protokolü hello istemci protokolü parametresi ayarlanmalıdır çok**MQTT**. Varsayılan olarak, hello cihaz SDK'ları bağlamak tooan IOT Hub ile Merhaba **CleanSession** bayrağı ayarlanmış çok**0** ve **QoS 1** hello IOT hub ile ileti alışverişi için.

Bir aygıt bağlı tooan IOT hub'ı olduğunda hello cihaz SDK'ları hello aygıt toosend iletileri tooand IOT hub'ından iletileri Al sağlayan yöntemler sağlar.

Her desteklenen dil ve hello parametresi toouse tooestablish bağlantı tooIoT Hub belirtir hello aşağıdaki tabloda bağlantıları toocode örnekleri içeren hello MQTT protokolünü kullanarak.

| Dil | Protokol parametresi |
| --- | --- |
| [Node.js][lnk-sample-node] |Azure-IOT-cihaz-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Cihaz uygulaması AMQP tooMQTT ' geçiş

Merhaba kullanıyorsanız [cihaz SDK'ları][lnk-device-sdks], AMQP kullanarak geçiş tooMQTT daha önce belirtildiği gibi hello Protokolü hello İstemci başlatması parametresinde değiştirilmesini gerektirir.

Bunu yaparken aşağıdaki öğelerindeki emin toocheck hello olun:

* MQTT hello bağlantıyı sonlandırır sırada AMQP birçok koşulları için hatalar döndürür. Sonuç olarak, özel durum mantığı işleme bazı değişiklikler gerektirebilir.
* MQTT hello desteklemediği *Reddet* alırken işlemleri [bulut-cihaz iletilerini][lnk-messaging]. Arka uç uygulamanızı tooreceive hello aygıt uygulamasından bir yanıt gerekirse, kullanmayı [doğrudan yöntemleri][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Merhaba MQTT protokolü kullanarak doğrudan
Bir aygıt hello cihaz SDK'ları kullanamıyorsanız, hala toohello ortak cihaz uç noktaları 8883 bağlantı noktasında hello MQTT protokolünü kullanarak bağlanabilir. Merhaba, **BAĞLAN** paket hello aygıt değerleri aşağıdaki hello kullanmalıdır:

* Hello için **ClientID** alanında, hello kullanın **DeviceID**.
* Hello için **kullanıcıadı** alanında, kullanmak `{iothubhostname}/{device_id}/api-version=2016-11-14`, {iothubhostname} olan hello burada hello IOT hub'ın tam CName.

    Örneğin, hello IOT hub'ınızın adını ise **contoso.azure devices.net** ve Cihazınızı hello adı ise **MyDevice01**, hello tam **kullanıcıadı** alan içermelidir `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Hello için **parola** alan, bir SAS belirteci kullanın. SAS belirteci hello Hello biçimi hello aynı hello HTTP ve AMQP protokolleri için:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Hakkında daha fazla bilgi için toogenerate SAS belirteci hello aygıt bölümüne bakın [IOT Hub'ı kullanarak güvenlik belirteçleri][lnk-sas-tokens].

    Test ederken hello de kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] aracı tooquickly kendi koda kopyalayıp bir SAS belirteci oluştur:

  1. Toohello Git **Yönetim** sekmesinde **aygıt Explorer**.
  2. Tıklatın **SAS belirteci** (sağ üst).
  3. Üzerinde **SASTokenForm**, aygıtınızı hello seçin **DeviceID** açılır. Ayarlama, **TTL**.
  4. Tıklatın **Generate** toocreate belirtecinizi.

     Merhaba oluşturulan SAS belirteci bu yapısının: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     Merhaba Bu belirteci toouse hello olarak parçası **parola** MQTT kullanarak alan tooconnect olduğu: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

İçin MQTT bağlanmak ve paketleri kesmek, IOT hub'ı sorunları olay hello olarak **işlemlerini izleme** kanal tootroubleshoot bağlantı sorunları yardımcı olabilecek ek bilgiler ile.

### <a name="sending-device-to-cloud-messages"></a>Cihaz bulut iletilerini gönderme

Başarılı bir bağlantı yaptıktan sonra bir cihaz iletileri tooIoT hub'ı kullanarak gönderebilirsiniz `devices/{device_id}/messages/events/` veya `devices/{device_id}/messages/events/{property_bag}` olarak bir **konu adı**. Merhaba `{property_bag}` öğesi Merhaba aygıt toosend iletileri url kodlanmış bir biçimde ek özellikleri sağlar. Örneğin:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Bu `{property_bag}` öğesi kullanır hello sorgu dizeleri hello HTTP protokolü için olduğu gibi aynı kodlama.
>
>

Merhaba cihaz uygulaması de kullanabilir `devices/{device_id}/messages/events/{property_bag}` hello olarak **Will konu adı** toodefine *iletilerini* toobe bir telemetri iletisi olarak iletilir.

- IOT hub'ı QoS 2 iletileri desteklemez. Cihaz uygulaması içeren bir ileti yayımlarsa **QoS 2**, IOT hub'ı hello ağ bağlantısı kapatır.
- IOT hub'ı tut iletileri kalmaz. Bir aygıt hello içeren bir ileti gönderirse **TUT** bayrağı ayarlanmış too1, IOT hub'ı ekler hello **x-opt-korumak** uygulama özelliği toohello iletisi. Bu durumda, ileti kalıcı hello yerine korumak, isteğe bağlı olarak IOT hub'ı toohello arka uç uygulama geçirir.
- IOT Hub, yalnızca cihaz başına bir etkin MQTT bağlantısını destekler. Yeni bir MQTT bağlantı adına hello aynı cihaz kimliği IOT hub'ı toodrop hello var olan bağlantının kesilmesine neden olur.

Daha fazla bilgi için bkz: [Geliştirici Kılavuzu Mesajlaşma][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Bulut-cihaz iletilerini alma

bir cihaz IOT hub'ı iletilerden tooreceive, abone kullanarak `devices/{device_id}/messages/devicebound/#` olarak bir **konu filtre**. birden çok düzeyli joker hello  **#**  tooallow hello yalnızca aygıt tooreceive ek özelliklerinde hello konu adı hello konu filtresi kullanılır. IOT hub'ı hello hello kullanımını izin verme  **#**  veya **?** alt konuları filtrelemek için joker karakter. IOT hub'ı genel amaçlı pub-sub Mesajlaşma Aracısı olmadığından, yalnızca belgelenen hello konu adları ve konu filtreleri destekler.

Merhaba tarafından temsil edilen tooits cihaza özel uç noktası başarıyla abone kadar hello cihaz tüm iletileri IOT Hub'ından almaz `devices/{device_id}/messages/devicebound/#` konu filtre. Başarılı abonelik kurulduktan sonra hello aygıtı tooit hello Abonelik başlangıç zamanından sonra gönderilen yalnızca bulut-cihaz iletilerini alma başlatır. Merhaba aygıt ile bağlanıyorsa **CleanSession** bayrağı ayarlanmış çok**0**, hello abonelik, farklı oturumlarında kalıcıdır. Bu durumda, ile sonraki bağlanışında hello **CleanSession 0** hello cihaz, bağlı değilken tooit gönderilen bekleyen iletileri alır. Merhaba aygıt kullanıyorsa **CleanSession** bayrağı ayarlanmış çok**1** tooits aygıt uç noktası abone kadar yine de, tüm iletileri IOT Hub'ından almaz.

IOT hub'ı sunar hello iletilerle **konu adı** `devices/{device_id}/messages/devicebound/`, veya `devices/{device_id}/messages/devicebound/{property_bag}` tüm ileti özellikleri varsa. `{property_bag}`İleti özelliklerini URL kodlanmış anahtar/değer çiftleri içerir. Yalnızca uygulama özellikleri ve kullanıcı ayarlanabilir Sistem Özellikleri (gibi **MessageID** veya **correlationıd değeri**) hello özellik paketindeki dahil edilir. Sistem özelliği adlara sahip hello önek  **$** , uygulama özellikleri ile önek hello özgün özellik adı kullanın.

Cihaz uygulaması tooa konuyla zaman abone olan **QoS 2**, IOT hub'ı verir hello maksimum QoS düzey 1 **SUBACK** paket. Bundan sonra QoS 1'i kullanarak iletileri toohello cihaz IOT hub'ı sunar.

### <a name="retrieving-a-device-twins-properties"></a>Bir cihaz çifti'nın özelliklerini alma

İlk olarak, bir cihaz çok abone`$iothub/twin/res/#`, tooreceive hello işlemin yanıtlar. Ardından, bir boş ileti tootopic gönderir `$iothub/twin/GET/?$rid={request id}`, için doldurulan bir değerle **istek kimliği**. hello hizmeti sonra konuda hello cihaz çifti verileri içeren bir yanıt iletisi gönderir `$iothub/twin/res/{status}/?$rid={request id}`, kullanma, hello aynı  **İstek Kimliği** hello istek olarak.

İstek Kimliği olarak başına bir ileti özellik değeri için geçerli bir değer olabilir [IOT Hub Geliştirici Kılavuzu Mesajlaşma][lnk-messaging], ve durumunu bir tamsayı olarak doğrulandı.
Merhaba yanıt gövdesi hello cihaz çifti hello özellikler bölümü içerir:

Merhaba kimlik kayıt defteri girişi Hello gövdesi toohello "Özellikler" üye, örneğin sınırlıdır:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

Merhaba olası durum kodları şunlardır:

|Durum | Açıklama |
| ----- | ----------- |
| 200 | Başarılı |
| 429 | (Kısıtlanan) çok sayıda istek, göre [IOT Hub'ın azaltma][lnk-quotas] |
| 5** | Sunucu hataları |

Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Cihaz çifti'nın bildirilen özelliklerini güncelleştir

Merhaba aşağıdaki sırayı bir aygıtı hello güncelleştirme biçimini açıklar IOT Hub cihaz çiftine hello özelliklerinde bildirdi:

1. Bir cihaz ilk toohello abone olmalısınız `$iothub/twin/res/#` IOT hub'dan konu tooreceive hello işlemin yanıtlar.

1. Bir aygıt hello cihaz çifti güncelleştirme toohello içeren bir ileti gönderir `$iothub/twin/PATCH/properties/reported/?$rid={request id}` konu. Bu iletiyi içeren bir **istek kimliği** değeri.

1. Konu bildirilen özellikler koleksiyonunda içeren bir yanıt iletisi için yeni ETag değeri hello gönderir hello sonra hizmet Hello `$iothub/twin/res/{status}/?$rid={request id}`. Bu yanıt iletisiyle kullandığı aynı hello **istek kimliği** hello istek olarak.

Merhaba istek ileti gövdesi yeni değerleri bildirilen özelliklerini (değiştirilebilir, başka bir özellik veya meta veri) sağlayan bir JSON belgesi içerir.
Merhaba JSON belgesi içindeki her üyenin güncelleştirir veya hello cihaz çifti'nın belgede hello karşılık gelen üye ekleyin. Bir üye kümesi çok`null`, hello nesnesini içeren hello üyeden siler. Örneğin:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Merhaba olası durum kodları şunlardır:

|Durum | Açıklama |
| ----- | ----------- |
| 200 | Başarılı |
| 400 | Hatalı istek. Hatalı biçimlendirilmiş JSON |
| 429 | (Kısıtlanan) çok sayıda istek, göre [IOT Hub'ın azaltma][lnk-quotas] |
| 5** | Sunucu hataları |

Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Alıcı istenen özellikler güncelleştirme bildirimlerini

Bir aygıt bağlandığında, IOT hub'ı bildirimleri toohello konu gönderir `$iothub/twin/PATCH/properties/desired/?$version={new version}`, hello çözüm arka ucu tarafından gerçekleştirilen hello güncelleştirme Merhaba içeriğine içerir. Örneğin:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Özelliği güncelleştirmeleri ettirilmesi `null` JSON hello değerleri anlamına gelir nesne üyesi siliniyor.


> [!IMPORTANT] 
> Yalnızca aygıtları bağlandığınızda IOT hub'ı değişiklik bildirimleri oluşturur. Tooimplement hello emin olun [aygıt yeniden bağlanmayı akış] [ lnk-devguide-twin-reconnection] tookeep hello istenen özellikleri IOT Hub ve hello cihaz uygulaması arasında eşitlenir.

Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Yanıt tooa doğrudan yöntemi

İlk olarak, bir aygıt toosubscribe çok sahip`$iothub/methods/POST/#`. IOT Hub yöntemi istekleri toohello konu gönderir `$iothub/methods/POST/{method name}/?$rid={request id}`, ya geçerli bir JSON ya da boş bir gövde ile.

toorespond, hello aygıt, geçerli bir JSON ya da boş gövde toohello konu içeren bir ileti gönderir `$iothub/methods/res/{status}/?$rid={request id}`, burada **istek kimliği** bir hello istek iletisinde hello toomatch sahiptir ve **durum** tamsayı toobe sahip .

Daha fazla bilgi için bkz: [yöntemi Geliştirici Kılavuzu doğrudan][lnk-methods].

### <a name="additional-considerations"></a>Diğer konular

Son yaparken, toocustomize hello MQTT protokol davranışı hello bulut tarafındaki gerekiyorsa hello gözden geçirmelidir [Azure IOT protokolü ağ geçidini] [ lnk-azure-protocol-gateway] toodeploy yüksek performans sağlayan doğrudan IOT Hub ile arabirimleri özel protokol ağ geçidi. Hello Azure IOT protokolü ağ geçidini, toocustomize hello aygıt Protokolü tooaccommodate brownfield MQTT dağıtımları veya diğer özel protokoller sağlar. Bu yaklaşım, ancak çalıştırın ve bir özel protokol ağ geçidi çalışmasını gerektirir.

## <a name="next-steps"></a>Sonraki adımlar

toolearn hello MQTT protokolü hakkında daha fazla bilgi görmek hello [MQTT belgelerine][lnk-mqtt-docs].

IOT hub'ı dağıtımınızı planlama hakkında daha fazla toolearn bakın:

* [IOT cihaz katalog için Azure Onaylandı][lnk-devices]
* [Destek ek protokoller][lnk-protocols]
* [Event Hubs ile karşılaştırın][lnk-compare]
* [Ölçeklendirme, HA ve DR][lnk-scaling]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
