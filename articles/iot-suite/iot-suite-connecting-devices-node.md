---
title: "Node.js kullanarak cihazı aaaConnect | Microsoft Docs"
description: "Nasıl tooconnect aygıt toohello Azure IOT paketi Uzaktan izleme çözümü Node.js içinde yazılmış bir uygulama kullanarak önceden yapılandırılmış açıklar."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Uzaktan izleme çözümü (Node.js), cihaz toohello Bağlan
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Node.js örnek bir çözüm oluşturun

Bu Node.js sürümünü 0.11.5 sağlayın ya da daha sonra dağıtım makinenize yüklü. Çalıştırabilirsiniz `node --version` hello komut satırı toocheck hello sürüm.

1. Adlı bir klasör oluşturun **RemoteMonitoring** geliştirme makinenizde. Komut satırı ortamınızdaki toothis klasörüne gidin.

1. Aşağıdaki çalışma hello toocomplete hello örnek uygulaması gereken toodownload ve yükleme hello paketleri komutlar:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Merhaba, **RemoteMonitoring** klasörünü adlı bir dosya oluşturun **remote_monitoring.js**. Bu dosyayı bir metin düzenleyicisinde açın.

1. Merhaba, **remote_monitoring.js** dosya, hello aşağıdakileri ekleyin `require` deyimleri:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Değişken bildirimleri hello sonra aşağıdaki hello eklemek `require` deyimleri. Yerine Hello yer tutucu değerler [aygıt kimliği] ve [aygıt anahtarı] aygıtınızın hello Uzaktan izleme çözüm panosunu not ettiğiniz değerlerle. Merhaba çözüm Panosu tooreplace [Iothub adı] öğesinden Hello IOT Hub ana bilgisayar adı kullanın. Örneğin, IoT Hub Ana Bilgisayar Adınız **contoso.azure-devices.net** şeklindeyse [IoTHub Adı] yerine **contoso** yazın:

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Değişkenleri toodefine aşağıdaki hello bazı temel telemetri verileri ekleyin:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Yardımcı işlevi tooprint işlem sonuçları aşağıdaki hello ekleyin:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Yardımcı işlevi toouse toorandomize hello telemetri değerleri aşağıdaki hello ekleyin:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Merhaba tanımı aşağıdaki hello eklemek **Deviceınfo** nesne hello cihaz başlangıçta gönderir:

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. Merhaba aşağıdakileri ekleyin tanımı hello cihaz çifti için bildirilen değerler. Bu tanım hello doğrudan yöntemleri hello aygıt destekler açıklamalarını içerir:

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. İşlev toohandle hello aşağıdaki hello eklemek **yeniden** doğrudan yöntem çağrısı:

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. İşlev toohandle hello aşağıdaki hello eklemek **InitiateFirmwareUpdate** doğrudan yöntem çağrısı. Zaman uyumsuz olarak başlatır hello cihazdaki üretici yazılımı güncelleştirmesi hello ve hello bellenim görüntü toodownload parametresi toospecify hello konumunu doğrudan bu yöntemi kullanır:

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. Kod toocreate istemci örneği aşağıdaki hello ekleyin:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Hello aşağıdaki kodu ekleyin:

    * Merhaba bağlantı açın.
    * Merhaba Gönder **Deviceınfo** nesnesi.
    * İstenen özellikleri için bir işleyici ayarlayın.
    * Bildirilen özellikleri gönderin.
    * Merhaba doğrudan yöntemleri için işleyiciler kaydedin.
    * Telemetri göndermeye başlayın.

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. Merhaba değişiklikleri toohello kaydetmek **remote_monitoring.js** dosya.

1. Komutu bir komut istemi toolaunch hello örnek uygulama aşağıdaki hello çalıştırın:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
