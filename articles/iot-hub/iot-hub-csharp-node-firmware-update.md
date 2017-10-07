---
title: "Azure IOT hub'ı (.NET/düğümü) aaaDevice ürün yazılımı güncelleştirmesini | Microsoft Docs"
description: "Azure IOT Hub tooinitiate cihaz üretici yazılımı toouse cihaz yönetimini nasıl güncelleştirin. Node.js tooimplement sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sı ve hello .NET tooimplement hello bellenim güncelleştirme tetikleyen bir hizmet uygulaması için Azure IOT hizmeti SDK'sını kullanın."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Aygıt Yönetimi tooinitiate aygıt üretici yazılımı güncelleştirmesi (.NET/düğüm) kullanın
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Giriş
Merhaba, [aygıt Management'i kullanmaya başlama] [ lnk-dm-getstarted] öğretici, gördüğünüz nasıl toouse hello [cihaz çifti] [ lnk-devtwin] ve [doğrudan yöntemleri] [ lnk-c2dmethod] temelleri tooremotely bir aygıtı yeniden başlatın. Bu öğretici kullandığı aynı IOT hub'ı temelleri hello ve nasıl toodo bir uçtan uca bellenim güncelleştirme benzetimli gösterir.  Bu desen Merhaba hello bellenim güncelleştirme uygulamasında kullanılan [Raspberry Pi'yi cihaz uygulaması örnek][lnk-rpi-implementation].

Bu öğretici şunların nasıl yapıldığını gösterir:

* IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello firmwareUpdate doğrudan yöntemini çağıran bir .NET konsol uygulaması oluşturun.
* Arabirimini uygulayan bir sanal cihaz uygulaması oluşturma bir **firmwareUpdate** doğrudan yöntemi. Bu yöntem, toodownload hello bellenim görüntü bekler, hello bellenim görüntüyü indirir ve son olarak hello bellenim görüntü geçerlidir bir çok aşama işlemi başlatır. Merhaba güncelleştirme her aşaması sırasında hello aygıt kullanır hello ilerlemeyi özellikleri tooreport bildirdi.

Bu öğretici Hello sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:

**dmpatterns_fwupdate_service.js**hello sanal cihaz uygulamada, doğrudan bir yöntem çağıran görüntüler hello yanıt ve düzenli aralıklarla (her 500ms) güncelleştirilmiş görüntüler hello bildirilen özellikleri.

**TriggerFWUpdate**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan firmwareUpdate doğrudan bir yöntem alır, bellenim güncelleştirme dahil çok durumlu işlem toosimulate çalıştırır: hello görüntü yükleme bekleniyor Merhaba yeni görüntüsü ve son olarak uygulanan hello görüntüsü yükleniyor.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü <br/>  [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

Merhaba izleyin [aygıt Management'i kullanmaya başlama](iot-hub-csharp-node-device-management-get-started.md) toocreate IOT hub'ınızı makalesi ve IOT Hub bağlantı dizenizi alın.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Merhaba cihaz doğrudan bir yöntem kullanarak bir uzak bellenim güncelleştirme Tetikle
Bu bölümde, bir cihazda uzaktan yazılımı güncelleştirmesi başlatır (C# kullanarak) bir .NET konsol uygulaması oluşturun. doğrudan yöntemi tooinitiate hello güncelleştirmesi Hello uygulamanın kullandığı ve kullandığı cihaz çifti sorguları tooperiodically hello hello etkin bellenim güncelleştirme durumunu alın.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Ad hello proje **TriggerFWUpdate**.

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

1. Çözüm Gezgini'nde hello sağ **TriggerFWUpdate** proje ve ardından **NuGet paketlerini Yönet...** .
1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip birden çok yer tutucu değerlerini hello hello ve hello Cihazınızı kimliğini değiştirin.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **TriggerFWUpdate** projedir **Başlat**.

1. Merhaba çözümü oluşturun.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Visual Studio'da hello üzerinde sağ **TriggerFWUpdate** projectRun toohello C# konsol uygulaması, select **hata ayıklama** ve **başlangıç yeni örnek**.

3. Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.

    ![Bellenim başarıyla güncelleştirildi][img-fwupdate]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide kullandığınız doğrudan yöntemi tootrigger uzak bir cihaz ve kullanılan hello bellenim güncelleştirme özellikleri toofollow hello hello bellenim güncelleştirme ilerlemesini bildirdi.

toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/