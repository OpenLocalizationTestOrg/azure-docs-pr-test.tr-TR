---
title: "Azure IOT hub'ı (düğüm) aaaSchedule işleriyle | Microsoft Docs"
description: "Nasıl tooschedule Azure IOT hub'ı işi tooinvoke birden çok aygıta doğrudan bir yöntem. Node.js tooimplement benzetimli hello cihaz uygulamaları ve hizmet uygulaması toorun hello işi için hello Azure IOT SDK'ları kullanın."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>Zamanlama ve yayın işleri (düğüm)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Azure IOT hub'ı, arka uç uygulama toocreate sağlayan tam olarak yönetilen bir hizmet ve zamanlama ve milyonlarca cihaza güncelleştirme izleme işleri ' dir.  İşlerini Merhaba aşağıdaki eylemler kullanılabilir:

* İstenen özellikleri güncelleştirme
* Güncelleştirme etiketleri
* Doğrudan yöntemleri çağırma

Kavramsal olarak, bir işi şu eylemlerden birini sarmalar ve bir cihaz çifti sorgu tarafından tanımlanan bir dizi aygıtlar, yürütme ilerlemesini parçaları hello.  Örneğin, bir cihaz çifti sorgu tarafından belirtilen ve gelecek bir zamanda zamanlanmış 10.000 cihaz üzerinde bir arka uç uygulaması iş tooinvoke yeniden başlatma yöntemini kullanabilirsiniz.  Bu cihazların her biri almak ve execute hello yeniden başlatma yöntemi olarak bu uygulama daha sonra ilerleme durumunu izleyebilirsiniz.

Bu makaleler, bu özelliklerin her biri hakkında daha fazla bilgi edinin:

* Cihaz çifti ve özellikleri: [cihaz çiftlerini ile çalışmaya başlama] [ lnk-get-started-twin] ve [Öğreticisi: nasıl toouse cihaz çifti özellikleri][lnk-twin-props]
* doğrudan yöntemleri: [IOT Hub Geliştirici Kılavuzu - doğrudan yöntemleri] [ lnk-dev-methods] ve [Öğreticisi: doğrudan yöntemleri][lnk-c2d-methods]

Bu öğretici şunların nasıl yapıldığını gösterir:

* Sağlayan doğrudan bir yönteme sahip bir sanal cihaz uygulaması oluşturma **lockDoor** hangi çağrılabilir hello çözüm arka ucu tarafından.
* Bu çağrı hello bir Node.js konsol uygulaması oluşturmak **lockDoor** hello sanal cihaz uygulamasının iş ve güncelleştirmeleri hello kullanarak doğrudan yönteminde istenen cihaz işi kullanarak özellikleri.

Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:

**simDevice.js**, tooyour IOT hub'ı hello cihaz kimliği bağlanır ve alan bir **lockDoor** doğrudan yöntemi.

**scheduleJobService.js**, çağıran doğrudan bir yöntem hello sanal cihaz uygulama ve güncelleştirme hello aygıt bir iş kullanarak twin'ın istenen özellikleri.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü <br/>  [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde, sanal cihaz yeniden başlatma tetikler hello bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturun ve Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullandığı hello rapor.

1. Adlı yeni bir boş klasör oluşturun **simDevice**.  Merhaba, **simDevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.  Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **simDevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt** paketi:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **simDevice.js** hello dosyasında **simDevice** klasör.
4. Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **simDevice.js** dosyası:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. İşlev toohandle hello aşağıdaki hello eklemek **lockDoor** yöntemi.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Kod tooregister hello işleyici hello için aşağıdaki hello eklemek **lockDoor** yöntemi.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Kaydet ve Kapat hello **simDevice.js** dosya.

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>İşlerini doğrudan bir yöntemi çağırmak ve bir cihaz çifti'nın özelliklerini güncelleştirmek için zamanla
Bu bölümde, bir uzak başlatan bir Node.js konsol uygulaması oluşturma **lockDoor** bir doğrudan yöntemi ve güncelleştirme hello cihaz çifti'nın özelliklerini kullanarak bir cihazdaki.

1. Adlı yeni bir boş klasör oluşturun **scheduleJobService**.  Merhaba, **scheduleJobService** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.  Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **scheduleJobService** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **scheduleJobService.js** hello dosyasında **scheduleJobService** klasör.
4. Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_gscheduleJobServiceetstarted_service.js** dosyası:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Değişken bildirimleri aşağıdaki hello ekleyin ve hello yer tutucu değerlerini değiştirin:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Kullanılan toomonitor hello hello işinin yürütülmesi olacaktır işlevi aşağıdaki hello ekleyin:
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. Hello aygıt yöntemini çağıran kodu tooschedule hello işi aşağıdaki hello ekleyin:
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. Kod tooschedule hello iş tooupdate hello cihaz çifti aşağıdaki hello ekleyin:
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. Kaydet ve Kapat hello **scheduleJobService.js** dosya.

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba hello komut isteminde **simDevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.
   
    ```
    node simDevice.js
    ```
2. Merhaba hello komut isteminde **scheduleJobService** klasörü, komut tootrigger hello işleri toolock hello kapı ve güncelleştirme hello çifti aşağıdaki hello çalıştırın
   
    ```
    node scheduleJobService.js
    ```
3. Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir iş tooschedule doğrudan yöntemi tooa cihaz ve hello güncelleştirme hello cihaz çifti'nın özelliklerinin kullanılır.

IOT Hub ve cihaz yönetim desenleri uzaktan gibi hello hava bellenim güncelleştirme kullanmaya Başlarken toocontinue bakın:

[Öğretici: Toodo üretici yazılımı nasıl güncelleştirin.][lnk-fwupdate]

IOT Hub ile çalışmaya başlama toocontinue bkz [Azure IOT Edge ile çalışmaya başlama][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
