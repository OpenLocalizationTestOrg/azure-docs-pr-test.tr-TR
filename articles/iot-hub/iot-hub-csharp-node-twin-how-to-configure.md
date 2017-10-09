---
title: "aaaUse Azure IOT Hub cihaz çifti özellikleri (.NET/düğümü) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz tooconfigure cihaz çiftlerini. Node.js tooimplement sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sı ve hello .NET tooimplement cihaz çifti kullanarak bir aygıt yapılandırmasını değiştirir bir hizmet uygulaması için Azure IOT hizmeti SDK'sını kullanın."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>İstenen özelliklerde tooconfigure aygıtları'nı kullanın
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Bu öğreticinin Hello sonunda, iki konsol uygulamaları olacaktır:

* **SimulateDeviceConfiguration.js**, istenen yapılandırma güncelleştirmesi bekler ve benzetimli yapılandırma güncellemeyi hello durumunu raporlar sanal cihaz uygulaması.
* **SetDesiredConfigurationAndQuery**hello ayarlar .NET arka uç uygulaması istenen bir cihazda yapılandırma ve sorguları hello yapılandırma güncelleştirme işlemi.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.
> 
> 

toocomplete hello aşağıdaki gereksinim Bu öğretici:

* Visual Studio 2015 veya Visual Studio 2017.
* Node.js 0.10.x sürümü veya sonraki bir sürüm.
* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.

Merhaba izlediyseniz [cihaz çiftlerini ile çalışmaya başlama] [ lnk-twin-tutorial] öğretici, zaten sahip olduğunuz bir IOT hub ve adlı bir cihaz kimliği **myDeviceId**. Bu durumda, toohello atlayabilirsiniz [oluşturma hello sanal cihaz uygulamasının] [ lnk-how-to-configure-createapp] bölümü.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Merhaba sanal cihaz uygulaması oluşturma
Bu bölümde, tooyour hub olarak bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**, istenen yapılandırma güncelleştirmesi bekler ve daha sonra güncelleştirmeleri benzetimli hello yapılandırmasını güncelleştirme işlemi raporlar.

1. Adlı yeni bir boş klasör oluşturun **simulatedeviceconfiguration**. Merhaba, **simulatedeviceconfiguration** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun. Tüm hello Varsayılanları kabul edin.
   
    ```
    npm init
    ```
1. Merhaba, komut isteminde **simulatedeviceconfiguration** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt**paketler:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SimulateDeviceConfiguration.js** hello dosyasında **simulatedeviceconfiguration** klasör.
1. Kod toohello aşağıdaki hello eklemek **SimulateDeviceConfiguration.js** dosya ve hello yerine **{cihaz bağlantı dizesi}** ne zaman kopyaladığınız hello cihaz bağlantı dizesiyle yer tutucu, Merhaba oluşturulan **myDeviceId** cihaz kimliği:
   
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
   
    Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile tüm hello yöntemleri gerekli toointeract kullanıma sunar. Bu kod hello başlatır **istemci** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve üzerinde hello güncelleştirme için bir işleyici ekler *özelliklerini istenen*. Merhaba işleyici olmadığını hello configIds karşılaştırarak bir gerçek yapılandırma değişikliği isteği olup, ardından hello yapılandırmasında değişiklik başlatan bir yöntemi çağırır doğrular.
   
    Basitlik Hello artırmak amacıyla için bu kodu sabit kodlanmış bir varsayılan hello ilk yapılandırmasını kullandığına dikkat edin. Gerçek bir uygulama büyük olasılıkla bu yapılandırma yerel depolama biriminden yüklenir.
   
   > [!IMPORTANT]
   > İstenen özellik değiştirme olayları her zaman bir kez aygıt bağlantıdaki gösterilen. Herhangi bir işlem gerçekleştirmeden önce özellikleri hello gerçek bir değişiklik olduğunu toocheck istenen emin olun.
   > 
   > 
1. Merhaba önce yöntemler aşağıdaki hello eklemek `client.open()` çağırma:
   
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
   
    Merhaba **initConfigChange** yöntemi güncelleştirmeleri hello bildirilen nesnesindeki özellikleri hello yerel cihaz çifti hello yapılandırmasıyla güncelleştirme isteği ve kümelerini hello durumu çok**bekleyen**, sonra güncelleştirmeleri hello cihaz çifti hello hizmeti. Merhaba cihaz çifti başarıyla güncelleştirdikten sonra içinde hello yürütülmesi sonlandırır uzun süre çalışan bir işlem benzetim **completeConfigChange**. Bu yöntem hello yerel bildirilen özellikleri hello durumu çok ayarlanırken güncelleştirmeleri**başarı** ve hello kaldırma **pendingConfig** nesnesi. Ardından, hello cihaz çifti hello hizmetinde güncelleştirir.
   
    Toosave bant genişliği, rapor özelliklerini yalnızca hello özellikleri toobe değiştiren belirterek güncelleştirilir unutmayın (adlı **düzeltme eki** kodu yukarıdaki hello içinde), hello tüm belgeyi değiştirme yerine.
   
   > [!NOTE]
   > Bu öğretici herhangi davranışı eşzamanlı yapılandırma güncelleştirmelerini benzetimini değil. Merhaba güncelleştirme çalışırken bazı yapılandırma güncelleştirme işlemleri hedef yapılandırmasının mümkün tooaccommodate değişiklikler olabilir, bazı ve bazı bunları bir hata durumu reddedebilirsiniz tooqueue olabilir. Belirli bir yapılandırma işlemi için istenen davranışı hello ve hello yapılandırma değişikliği başlatmadan önce hello uygun mantığı ekleyin emin tooconsider olun.
   > 
   > 
1. Merhaba cihaz uygulaması çalıştırın:
   
        node SimulateDeviceConfiguration.js
   
    Merhaba iletiyi görmeniz gerekir `retrieved device twin`. Çalışan hello uygulama tutun.

## <a name="create-hello-service-app"></a>Merhaba service uygulaması oluşturma
Bu bölümde, bu güncelleştirmeleri hello bir .NET konsol uygulaması oluşturacak *özelliklerini istenen* hello cihaz çifti ile ilişkili üzerinde **myDeviceId** ile yeni bir telemetri yapılandırma nesnesi. Ardından hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve hello hello birbirinden istenen ve hello cihaz yapılandırmalarını bildirilen gösterir.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Ad hello proje **SetDesiredConfigurationAndQuery**.
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. Çözüm Gezgini'nde hello sağ **SetDesiredConfigurationAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .
1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    Merhaba **kayıt defteri** nesne cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar. Bu kod hello başlatır **kayıt defteri** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve ardından yeni bir telemetri yapılandırma nesnesi ile istenen özelliklerini güncelleştirir.
    Bundan sonra 10 saniyede hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve baskı siparişi hello istenen ve telemetri yapılandırmaları bildirdi. Toohello başvuran [IOT hub'ı sorgu dili] [ lnk-query] nasıl toogenerate zengin raporları, tüm aygıtlarda toolearn.
   
   > [!IMPORTANT]
   > Bu uygulama yalnızca tanım amaçlıdır her 10 saniye IOT hub'ı sorgular. Kullanım toogenerate kullanıcı dönük raporları birçok cihaz ve toodetect değişiklikleri arasında sorgular. Çözümünüz cihaz olayların gerçek zamanlı bildirimler gerektiriyorsa, kullanın [twin bildirimleri][lnk-twin-notifications].
   > 
   > 
1. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **SetDesiredConfigurationAndQuery** projedir **Başlat**. Merhaba çözümü oluşturun.
1. İle **SimulateDeviceConfiguration.js** , Merhaba .NET uygulaması Visual Studio kullanarak çalıştırma **F5** ve hello bildirilen yapılandırma çıkarılıp görmelisiniz. **başarı** çok**bekleyen** çok**başarı** hello yeni etkin ile 24 saat yerine beş dakikalık sıklığı yeniden gönderin.

 ![Cihaz başarıyla yapılandırıldı][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Merhaba aygıt rapor işlemi hello sorgu sonucu arasındaki tooa minute yukarı bir gecikme yoktur. Çok yüksek ölçekli tooenable hello sorgu altyapısı toowork budur. tooretrieve tutarlı bir tek cihaz çifti görünümlerini kullanın hello **getDeviceTwin** hello yönteminde **kayıt defteri** sınıfı.
   > 
   > 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, istenen yapılandırma olarak kümesi *özellikleri istenen* hello çözümden arka uç ve değiştirebilir ve durumunu bildirilen hello aracılığıyla raporlama çok adımlı güncelleştirme işleminin benzetimini cihaz uygulama toodetect yazıldı Özellikler.

Kaynakları toolearn nasıl aşağıdaki kullanım hello için:

* Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici
* zamanlama veya gerçekleştirmek aygıtların büyük kümeleri üzerinde işlemler bkz hello [zamanlama ve yayın işleri] [ lnk-schedule-jobs] Öğreticisi.
* Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
