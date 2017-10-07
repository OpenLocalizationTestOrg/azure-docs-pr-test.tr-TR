---
title: "aaaGet başlatılan Azure IOT Hub cihaz çiftlerini (düğüm) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz çiftlerini tooadd etiketleri ve IOT Hub sorgusuyla kullanın. Node.js tooimplement hello sanal cihaz uygulaması için Azure IOT SDK'ları hello ve hello etiketleri ekler ve hello IOT hub'ı sorgu çalışan bir hizmet uygulaması kullanın."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Cihaz çiftlerini (düğüm) ile çalışmaya başlama
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları olacaktır:

* **AddTagsAndQuery.js**, etiketleri ekler ve cihaz çiftlerini sorgular bir Node.js arka uç uygulaması.
* **TwinSimulatedDevice.js**, bir cihaza benzetim yapan tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve kendi bağlantı koşulu raporları bir Node.js uygulaması.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.
> 
> 

toocomplete hello aşağıdaki gereksinim Bu öğretici:

* Node.js 0.10.x sürümü veya sonraki bir sürüm.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Merhaba service uygulaması oluşturma
Bu bölümde, konum meta veri toohello cihaz çifti ile ilişkili ekler bir Node.js konsol uygulaması oluşturma **myDeviceId**. Ardından hello cihaz çiftlerini hello IOT hub'ı hello bulunan hello aygıtları seçerek BİZE depolanır ve bir cep telefonu bağlantı raporlama olanları hello sorgular.

1. Adlı yeni bir boş klasör oluşturun **addtagsandqueryapp**. Merhaba, **addtagsandqueryapp** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **addtagsandqueryapp** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** paketi:
   
    ```
    npm install azure-iothub --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **AddTagsAndQuery.js** hello dosyasında **addtagsandqueryapp** klasör.
4. Aşağıdaki kodu toohello hello eklemek **AddTagsAndQuery.js** dosya ve hello yerine **{IOT hub bağlantı dizesine}** yer tutucu hello hub'ınızı oluşturduğunuzda kopyaladığınız IOT Hub bağlantı dizesine sahip:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Merhaba **kayıt defteri** nesne cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar. Merhaba önceki kod ilk hello başlatır **kayıt defteri** nesnesi alır cihaz çiftinin hello sonra **myDeviceId**ve son olarak, etiketleri istenen hello konumu bilgilerle güncelleştirir.
   
    Merhaba sonra hello güncelleştirme onu çağrıları hello etiketler **queryTwins** işlevi.
5. Merhaba ucunda koddan hello eklemek **AddTagsAndQuery.js** tooimplement hello **queryTwins** işlevi:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    Merhaba önceki kod iki sorguları çalıştırır: hello ilk yalnızca hello cihaz çiftlerini hello bulunan aygıtların seçer **Redmond43** tesis ve ayrıca üzerinden bağlanan hello ikinci iyileştirir hello sorgu tooselect yalnızca hello cihazları cep telefonu şebekesi.
   
    Merhaba oluşturduğunda bu hello önceki kod Not **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir. Merhaba **sorgu** nesnesini içeren bir **hasMoreResults** tooinvoke hello kullanabileceğiniz boolean özelliği **nextAsTwin** yöntemleri tooretrieve tüm sonuçları birden çok kez. Bir yöntem olarak adlandırılan **sonraki** Örneğin, cihaz çiftlerini toplama sorguların sonuçlarını olmayan sonuçlar için kullanılabilir.
6. Merhaba uygulaması ile çalıştırın:
   
        node AddTagsAndQuery.js
   
    Bulunan tüm cihazlar için sorgu hello soran bir cihazda hello sonuçlarında görmelisiniz **Redmond43** ve hiçbiri hello kısıtlayan hello sorgu için bir cep telefonu şebekesi kullanmak toodevices sonuçlanır.
   
    ![][1]

Merhaba sonraki bölümde hello bağlantı bilgilerini raporları bir cihaz uygulaması oluşturma ve değişiklikleri hello önceki bölümdeki hello sorgusunun sonucu hello.

## <a name="create-hello-device-app"></a>Merhaba cihaz uygulaması oluşturma
Bu bölümde, tooyour hub olarak bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**ve ardından, cihaz çifti bir cep telefonu şebekesi kullanarak bağlı özellikler toocontain hello bilgilerini bildirilen güncelleştirmeler.

> [!NOTE]
> Şu anda cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak. Lütfen toohello bakın [MQTT Destek] [ lnk-devguide-mqtt] hakkında yönergeler için makalenin tooconvert mevcut aygıt uygulama toouse MQTT.
> 
> 

1. Adlı yeni bir boş klasör oluşturun **reportconnectivity**. Merhaba, **reportconnectivity** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **reportconnectivity** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz**, ve **azure-IOT-cihaz-mqtt** paketi :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **ReportConnectivity.js** hello dosyasında **reportconnectivity** klasör.
4. Kod toohello aşağıdaki hello eklemek **ReportConnectivity.js** dosya ve hello yerine **{cihaz bağlantı dizesi}** hello oluşturduğunuzda kopyaladığınız hello cihaz bağlantı dizesiyle yer tutucusu **myDeviceId** cihaz kimliği:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile toointeract duyduğunuz tüm hello yöntemler sunar. Merhaba başlatır sonra önceki kod Hello **istemci** nesnesi alır, cihaz çiftinin hello **myDeviceId** ve kendi bildirilen özelliği hello bağlantı bilgileriyle güncelleştirir.
5. Merhaba cihaz uygulamayı çalıştırma
   
        node ReportConnectivity.js
   
    Merhaba iletiyi görmeniz gerekir `twin state reported`.
6. Merhaba aygıt bildirilen bağlantı bilgilerini, her iki sorgularda görüntülenmelidir. Merhaba edilene gidin **addtagsandqueryapp** klasörü ve Çalıştır hello sorgular yeniden:
   
        node AddTagsAndQuery.js
   
    Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.
   
    ![][3]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve bir sanal cihaz uygulaması tooreport aygıt bağlantı bilgilerini hello cihaz çiftine yazıldı. Ayrıca nasıl öğrenilen tooquery hello SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri.

Kaynakları toolearn nasıl aşağıdaki kullanım hello için:

* Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici
* cihaz çifti'nın istenen özellikleri ile hello kullanarak cihazları yapılandırma [kullanım istenen özellikleri tooconfigure aygıtları] [ lnk-twin-how-to-configure] öğretici,
* Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
