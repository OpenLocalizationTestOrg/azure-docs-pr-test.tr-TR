---
title: "aaaGet başlatılan ile Azure IOT Hub cihaz Yönetimi (.NET/düğümü) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz Yönetimi tooinitiate uzaktaki bir aygıtı yeniden başlatın. Node.js tooimplement doğrudan yöntemi ve hello .NET tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>Aygıt Yönetimi (.NET/düğümü) ile çalışmaya başlama

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Bu öğretici şunların nasıl yapıldığını gösterir:

* IOT hub'ınızda bir cihaz kimliği oluşturma ve Hello Azure portal toocreate IOT hub'ı kullanın.
* Bu cihazı yeniden başlatır doğrudan bir yöntem içeren bir sanal cihaz uygulaması oluşturursunuz. Doğrudan yöntemleri hello buluttan çağrılır.
* IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello yeniden başlatma doğrudan yöntemini çağıran bir .NET konsol uygulaması oluşturun.

Bu öğretici Hello sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:

**dmpatterns_getstarted_device.js**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan bir yeniden başlatma doğrudan yöntemi alır fiziksel yeniden başlatma taklit eder ve hello son yeniden başlatma için başlangıç zamanı raporlar.

**TriggerReboot**, doğrudan bir yöntem hello sanal cihaz uygulamada, çağıran hello yanıt görüntüler ve güncelleştirilmiş görüntüler hello rapor özellikleri.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü <br/>  [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Tetikleyici doğrudan bir yöntem kullanarak hello cihazda Uzaktan yeniden başlatma
Bu bölümde, doğrudan bir yöntem kullanarak bir cihazda Uzaktan yeniden başlatma başlatır (C# kullanarak) bir .NET konsol uygulaması oluşturun. Merhaba uygulaması bu cihaz için cihaz çifti sorguları toodiscover hello son yeniden başlatma zamanı kullanır.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi tooa yeni çözüm Ekle **konsol uygulaması (.NET Framework)** proje şablonu. Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü. Ad hello proje **TriggerReboot**.

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

2. Çözüm Gezgini'nde hello sağ **TriggerReboot** proje ve ardından **NuGet paketlerini Yönet**.
3. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
4. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba hello önceki bölümde ve hello hedef aygıt oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.  Bu kod alır hello cihaz çifti hello cihaz ve çıkışları hello yeniden başlatıldığı için özellikler bildirdi.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.  Bu kod, doğrudan bir yöntem kullanarak hello aygıtta hello yeniden başlatır.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Merhaba çözümü oluşturun.

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde şunları yapacaksınız:

* Merhaba bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturma
* Tetikleyici sanal cihaz yeniden başlatma
* Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullanım hello bildirdi

1. Adlı yeni bir boş klasör oluşturun **manageddevice**.  Merhaba, **manageddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.  Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **manageddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **dmpatterns_getstarted_device.js** hello dosyasında **manageddevice** klasör.
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
7. Merhaba aşağıdaki tooopen hello bağlantı tooyour IOT hub'ı kod ve hello doğrudan yöntemi dinleyicisini başlatmak ekleyin:
   
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


## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Çalışma hello C# konsol uygulaması **TriggerReboot**. Sağ hello **TriggerReboot** proje, select **hata ayıklama**ve ardından **başlangıç yeni örnek**.

3. Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/