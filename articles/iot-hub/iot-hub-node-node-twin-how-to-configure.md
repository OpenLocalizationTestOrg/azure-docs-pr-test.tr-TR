---
title: "aaaUse Azure IOT Hub cihaz çifti özellikleri (düğüm) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz tooconfigure cihaz çiftlerini. Sanal cihaz uygulaması ve cihaz çifti kullanarak bir aygıt yapılandırmasını değiştirir bir hizmet uygulaması hello Azure IOT SDK'ları için Node.js tooimplement kullanın."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Kullanmak istediğiniz özellikleri tooconfigure aygıtları (düğüm)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları olacaktır:

* **SimulateDeviceConfiguration.js**, istenen yapılandırma güncelleştirmesi bekler ve benzetimli yapılandırma güncellemeyi hello durumunu raporlar sanal cihaz uygulaması.
* **SetDesiredConfigurationAndQuery.js**hello ayarlar bir Node.js arka uç uygulaması istenen bir cihazda yapılandırma ve sorguları hello yapılandırma güncelleştirme işlemi.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.
> 
> 

toocomplete hello aşağıdaki gereksinim Bu öğretici:

* Node.js 0.10.x sürümü veya sonraki bir sürüm.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

Merhaba izlediyseniz [cihaz çiftlerini ile çalışmaya başlama] [ lnk-twin-tutorial] öğretici, zaten sahip olduğunuz bir IOT hub ve adlı bir cihaz kimliği **myDeviceId**; ve toohello atlayabilirsiniz[ Merhaba sanal cihaz uygulaması oluşturma] [ lnk-how-to-configure-createapp] bölümü.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Merhaba sanal cihaz uygulaması oluşturma
Bu bölümde, tooyour hub olarak bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**, istenen yapılandırma güncelleştirmesi bekler ve daha sonra güncelleştirmeleri benzetimli hello yapılandırmasını güncelleştirme işlemi raporlar.

1. Adlı yeni bir boş klasör oluşturun **simulatedeviceconfiguration**. Merhaba, **simulatedeviceconfiguration** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **simulatedeviceconfiguration** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz**, ve **azure-IOT-cihaz-mqtt**paketi:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SimulateDeviceConfiguration.js** hello dosyasında **simulatedeviceconfiguration** klasör.
4. Kod toohello aşağıdaki hello eklemek **SimulateDeviceConfiguration.js** dosya ve hello yerine **{cihaz bağlantı dizesi}** ne zaman kopyaladığınız hello cihaz bağlantı dizesiyle yer tutucu, Merhaba oluşturulan **myDeviceId** cihaz kimliği:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile tüm hello yöntemleri gerekli toointeract kullanıma sunar. Merhaba başlatır sonra önceki kod Hello **istemci** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve istenen özelliklerindeki hello güncelleştirme için bir işleyici ekler. Merhaba işleyici olmadığını hello configIds karşılaştırarak bir gerçek yapılandırma değişikliği isteği olup, ardından hello yapılandırmasında değişiklik başlatan bir yöntemi çağırır doğrular.
   
    Basitlik Hello artırmak amacıyla için sabit kodlanmış bir varsayılan hello önceki kod hello ilk yapılandırmasını kullandığını unutmayın. Gerçek bir uygulama büyük olasılıkla bu yapılandırma yerel depolama biriminden yüklenir.
   
   > [!IMPORTANT]
   > İstenen özellik değiştirme olayları her zaman bir kez aygıt bağlantıdaki gösterilen, herhangi bir işlem gerçekleştirmeden önce özellikleri hello gerçek bir değişiklik olduğunu toocheck istenen emin olun.
   > 
   > 
5. Merhaba önce yöntemler aşağıdaki hello eklemek `client.open()` çağırma:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Merhaba **initConfigChange** yöntemi güncelleştirmeleri hello yapılandırmasını güncelleştirme isteği olan hello yerel cihaz çifti nesneye özellikleri bildirilen ve ayarlar hello durumu çok**bekleyen**, aygıt güncelleştirmeleri hello sonra Merhaba hizmetinde çifti. Merhaba cihaz çifti başarıyla güncelleştirdikten sonra içinde hello yürütülmesi sonlandırır uzun süre çalışan bir işlem benzetim **completeConfigChange**. Bu yöntem güncelleştirmeleri hello yerel cihaz çifti özellikler hello durumu çok ayarlama bildirilen**başarı** ve hello kaldırma **pendingConfig** nesnesi. Ardından, hello cihaz çifti hello hizmetinde güncelleştirir.
   
    Toosave bant genişliği, rapor özelliklerini yalnızca hello özellikleri toobe değiştiren belirterek güncelleştirilir unutmayın (adlı **düzeltme eki** kodu yukarıdaki hello içinde), hello tüm belgeyi değiştirme yerine.
   
   > [!NOTE]
   > Bu öğretici herhangi davranışı eşzamanlı yapılandırma güncelleştirmelerini benzetimini değil. Merhaba güncelleştirme çalışırken bazı yapılandırma güncelleştirme işlemleri hedef yapılandırmasının mümkün tooaccommodate değişiklikler olabilir, diğerleri ve diğerleri bunları bir hata durumu reddedebilirsiniz tooqueue olabilir. Belirli bir yapılandırma işlemi için istenen davranışı hello ve hello yapılandırma değişikliği başlatmadan önce hello uygun mantığı ekleyin emin tooconsider olun.
   > 
   > 
6. Merhaba cihaz uygulaması çalıştırın:
   
        node SimulateDeviceConfiguration.js
   
    Merhaba iletiyi görmeniz gerekir `retrieved device twin`. Çalışan hello uygulama tutun.

## <a name="create-hello-service-app"></a>Merhaba service uygulaması oluşturma
Bu bölümde, bu güncelleştirmeleri hello bir Node.js konsol uygulaması oluşturacak *özelliklerini istenen* hello cihaz çifti ile ilişkili üzerinde **myDeviceId** ile yeni bir telemetri yapılandırma nesnesi. Ardından hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve hello hello birbirinden istenen ve hello cihaz yapılandırmalarını bildirilen gösterir.

1. Adlı yeni bir boş klasör oluşturun **setdesiredandqueryapp**. Merhaba, **setdesiredandqueryapp** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **setdesiredandqueryapp** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** paketi:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SetDesiredAndQuery.js** hello dosyasında **addtagsandqueryapp** klasör.
4. Aşağıdaki kodu toohello hello eklemek **SetDesiredAndQuery.js** dosya ve hello yerine **{IOT hub bağlantı dizesine}** yer tutucu hello hub'ınızı oluşturduğunuzda kopyaladığınız IOT Hub bağlantı dizesine sahip :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Merhaba **kayıt defteri** nesne cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar. Merhaba başlatır sonra önceki kod Hello **kayıt defteri** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve yeni bir telemetri yapılandırma nesnesi ile istenen özelliklerini güncelleştirir. Bundan sonra hello çağırır **queryTwins** 10 saniye olay işlev.

    > [!IMPORTANT]
    > Bu uygulama yalnızca tanım amaçlıdır her 10 saniye IOT hub'ı sorgular. Kullanım toogenerate kullanıcı dönük raporları birçok cihaz ve toodetect değişiklikleri arasında sorgular. Çözümünüz cihaz olayların gerçek zamanlı bildirimler gerektiriyorsa, kullanın [twin bildirimleri][lnk-twin-notifications].
    > 
    >.

1. Kod hemen hello önce aşağıdaki hello eklemek `registry.getDeviceTwin()` çağırma tooimplement hello **queryTwins** işlevi:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    cihaz çiftlerini hello IOT hub'da depolanan Hello önceki kod sorguları hello ve baskı siparişi hello istenen ve telemetri yapılandırmaları bildirdi. Toohello başvuran [IOT hub'ı sorgu dili] [ lnk-query] nasıl toogenerate zengin raporları, tüm aygıtlarda toolearn.
2. İle **SimulateDeviceConfiguration.js** , hello uygulamayla çalıştırma:
   
        node SetDesiredAndQuery.js 5m
   
    Merhaba bildirilen yapılandırma çıkarılıp görmelisiniz **başarı** çok**bekleyen** çok**başarı** hello yeni etkin 24 yerine beş dakikalık sıklığı yeniden gönderin saat.
   
   > [!IMPORTANT]
   > Merhaba aygıt rapor işlemi hello sorgu sonucu arasındaki tooa minute yukarı bir gecikme yoktur. Çok yüksek ölçekli tooenable hello sorgu altyapısı toowork budur. tooretrieve tutarlı bir tek cihaz çifti görünümlerini kullanın hello **getDeviceTwin** hello yönteminde **kayıt defteri** sınıfı.
   > 
   > 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, istenen yapılandırma olarak ayarlamak *özelliklerini istenen* bir arka uç uygulamasından ve değiştirebilir ve durumunu olarak raporlama çok adımlı güncelleştirme işleminin benzetimini bir sanal cihaz uygulaması toodetect yazdı  *Özellikler bildirilen* toohello cihaz çifti.

Kaynakları toolearn nasıl aşağıdaki kullanım hello için:

* Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici
* zamanlama veya gerçekleştirmek aygıtların büyük kümeleri üzerinde işlemler bkz hello [zamanlama ve yayın işleri] [ lnk-schedule-jobs] Öğreticisi.
* Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
