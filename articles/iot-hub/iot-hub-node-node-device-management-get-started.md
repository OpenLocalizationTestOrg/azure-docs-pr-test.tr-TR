---
title: "aaaGet başlatılan ile Azure IOT Hub cihaz Yönetimi (düğüm) | Microsoft Docs"
description: "Nasıl toouse IOT Hub cihaz Yönetimi tooinitiate uzaktaki bir aygıtı yeniden başlatın. Doğrudan bir yöntem içeren bir sanal cihaz uygulamasının ve hello doğrudan yöntemini çağıran bir hizmet uygulaması için Node.js tooimplement hello Azure IOT SDK'sını kullanın."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Aygıt Yönetimi (düğüm) ile çalışmaya başlama

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Bu öğretici şunların nasıl yapıldığını gösterir:

* IOT hub'ınızda bir cihaz kimliği oluşturma ve Hello Azure portal toocreate IOT hub'ı kullanın.
* Bu cihazı yeniden başlatır doğrudan bir yöntem içeren bir sanal cihaz uygulaması oluşturursunuz. Doğrudan yöntemleri hello buluttan çağrılır.
* IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello yeniden başlatma doğrudan yöntemini çağıran bir Node.js konsol uygulaması oluşturun.

Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:

**dmpatterns_getstarted_device.js**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan bir yeniden başlatma doğrudan yöntemi alır fiziksel yeniden başlatma taklit eder ve hello son yeniden başlatma için başlangıç zamanı raporlar.

**dmpatterns_getstarted_service.js**, doğrudan bir yöntem hello sanal cihaz uygulamada, çağıran hello yanıt görüntüler ve güncelleştirilmiş görüntüler hello rapor özellikleri.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü <br/>  [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde şunları yapacaksınız:

* Merhaba bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturma
* Tetikleyici sanal cihaz yeniden başlatma
* Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullanım hello bildirdi

1. **manageddevice** adlı boş bir klasör oluşturun.  Merhaba, **manageddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.  Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **manageddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **dmpatterns_getstarted_device.js** hello dosyasında **manageddevice** klasör.
4. Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_getstarted_device.js** dosyası:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.  Merhaba bağlantı dizesi, cihaz bağlantı dizesi ile değiştirin.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Merhaba aygıtta işlevi tooimplement hello doğrudan yöntemi aşağıdaki hello ekleme
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Merhaba bağlantı tooyour IOT hub'ı açın ve hello doğrudan yöntemi dinleyicisi başlayın:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Kaydet ve Kapat hello **dmpatterns_getstarted_device.js** dosya.

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Tetikleyici doğrudan bir yöntem kullanarak hello cihazda Uzaktan yeniden başlatma
Bu bölümde, doğrudan bir yöntem kullanarak bir cihazda Uzaktan yeniden başlatma başlatan bir Node.js konsol uygulaması oluşturun. Merhaba uygulaması bu cihaz için cihaz çifti sorguları toodiscover hello son yeniden başlatma zamanı kullanır.

1. Adlı bir boş klasör oluşturun **triggerrebootondevice**.  Merhaba, **triggerrebootondevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.  Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **triggerrebootondevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt** paketi:
   
    ```
    npm install azure-iothub --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **dmpatterns_getstarted_service.js** hello dosyasında **triggerrebootondevice** klasör.
4. Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_getstarted_service.js** dosyası:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Değişken bildirimleri aşağıdaki hello ekleyin ve hello yer tutucu değerlerini değiştirin:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. İşlev tooinvoke hello aygıt yöntemi tooreboot hello hedef aygıt aşağıdaki hello ekleyin:
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Merhaba aşağıdaki tooquery hello cihaz için işlev ve hello son yeniden başlatma zamanı alma ekleyin:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Merhaba tetiklemek kod toocall hello işlevleri aşağıdaki hello doğrudan yöntemi yeniden başlatın ve sorgu hello için son zaman yeniden ekleyin:
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Kaydet ve Kapat hello **dmpatterns_getstarted_service.js** dosya.

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Merhaba hello komut isteminde **triggerrebootondevice** komutu tootrigger hello uzaktan aşağıdaki hello Çalıştır klasörü yeniden başlatın ve hello cihaz çifti toofind hello en son yeniden başlatma için zaman sorgu.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
