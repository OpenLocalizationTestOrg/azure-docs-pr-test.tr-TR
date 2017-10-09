---
title: "Azure IOT hub'ı (.NET/düğümü) aaaSchedule işleriyle | Microsoft Docs"
description: "Nasıl tooschedule Azure IOT hub'ı işi tooinvoke birden çok aygıta doğrudan bir yöntem. Node.js tooimplement benzetimli hello cihaz uygulamaları ve hello .NET tooimplement bir hizmeti uygulama toorun hello işi için Azure IOT hizmeti SDK'sı için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Zamanlama ve yayın işleri (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Milyonlarca cihaza güncelleştirme Azure IOT Hub tooschedule ve izleme işlemlerini kullanın. İşlerini kullanın:

* İstenen özellikleri güncelleştirme
* Güncelleştirme etiketleri
* Doğrudan yöntemleri çağırma

Bir işi şu eylemlerden birini sarmalar ve cihaz çifti sorgu tarafından tanımlanan bir dizi cihazların yürütmeyi parçaları hello. Örneğin, bir arka uç uygulaması iş tooinvoke doğrudan bir yöntem hello aygıtları yeniden 10.000 cihazlarda kullanabilirsiniz. Cihaz hello kümesini içeren bir cihaz çifti sorgu belirtin ve gelecek bir zamanda hello iş toorun zamanlayın. Merhaba parçaları ilerleyişini her hello aygıtların almak ve hello yeniden başlatma doğrudan yöntemi yürütün.

Bu özelliklerin her biri hakkında daha fazla toolearn bakın:

* Cihaz çifti ve özellikleri: [cihaz çiftlerini ile çalışmaya başlama] [ lnk-get-started-twin] ve [Öğreticisi: nasıl toouse cihaz çifti özellikleri][lnk-twin-props]
* Doğrudan yöntemleri: [IOT Hub Geliştirici Kılavuzu - doğrudan yöntemleri] [ lnk-dev-methods] ve [Öğreticisi: doğrudan yöntemleri kullanın][lnk-c2d-methods]

Bu öğretici şunların nasıl yapıldığını gösterir:

* Adlı doğrudan bir yöntem uygulayan bir cihaz uygulaması oluşturma **lockDoor** hello arka uç uygulama tarafından çağrılabilir. Merhaba cihaz uygulaması istenen özellik değişikliklerini hello arka uç uygulamasını da alır.
* Bir iş toocall hello oluşturan bir arka uç uygulaması oluşturma **lockDoor** birden fazla cihazda yöntemi doğrudan. Başka bir iş, istenen özelliği toomultiple aygıtları güncelleştirir gönderir.

Bu öğretici Hello sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:

**simDevice.js** tooyour IOT hub'a bağlandığında, uygulayan hello **lockDoor** yöntemi ve tanıtıcıları istenen özellik değişikliklerini doğrudan.

**ScheduleJob** işleri toocall hello kullanan **lockDoor** doğrudan yöntemi ve güncelleştirme hello cihaz çifti istenen birden çok cihazı özellikleri.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Node.js 0.12.x sürümü veya sonraki bir sürüm. Merhaba makale [geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.
* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Doğrudan bir yöntem çağırma ve cihaz çifti güncelleştirmeleri göndermek için zamanlama işleri

Bu bölümde, işleri toocall hello kullanır (C# kullanarak) bir .NET konsol uygulaması oluşturma **lockDoor** doğrudan yöntemi ve istenen özelliği güncelleştirmeleri toomultiple aygıtları gönderin.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Ad hello proje **ScheduleJob**.

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

1. Çözüm Gezgini'nde hello sağ **ScheduleJob** proje ve ardından **NuGet paketlerini Yönet...** .
1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu adım indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Merhaba aşağıdakileri ekleyin `using` deyimi yoksa hello varsayılan deyimlerinde.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba yer tutucu hello hello önceki bölümde oluşturduğunuz hello hub için IOT Hub bağlantı dizesini değiştirin.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **ScheduleJob** projedir **Başlat**. Merhaba çözümü oluşturun.

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma

Bu bölümde, sanal cihaz yeniden başlatma tetikler hello bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturun ve Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullandığı hello rapor.

1. Adlı yeni bir boş klasör oluşturun **simDevice**.  Merhaba, **simDevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.  Tüm hello Varsayılanları kabul edin:

    ```cmd/sh
    npm init
    ```

1. Merhaba, komut isteminde **simDevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** paketler:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Bir metin düzenleyicisi kullanarak yeni bir oluşturma **simDevice.js** hello dosyasında **simDevice** klasör.

1. Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **simDevice.js** dosyası:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği. Değerleri uygun tooyour Kurulum emin tooreplace hello yer tutucularını olun.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. İşlev toohandle hello aşağıdaki hello eklemek **lockDoor** yöntemi.

    ```nodejs
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

1. Kod tooregister hello işleyici hello için aşağıdaki hello eklemek **lockDoor** yöntemi.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Kaydet ve Kapat hello **simDevice.js** dosya.

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba hello komut isteminde **simDevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.

    ```cmd/sh
    node simDevice.js
    ```

1. Çalışma hello C# konsol uygulaması **ScheduleJob** hello üzerinde sağ tıklanarak **ScheduleJob** sonra seçerek proje **hata ayıklama** ve **başlangıç yeni örnek**.

1. Cihaz ve arka uç uygulamaları hello çıktısını görürsünüz.

    ![Merhaba uygulamaları tooschedule işleri çalıştırma][img-schedulejobs]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir iş tooschedule doğrudan yöntemi tooa cihaz ve hello güncelleştirme hello cihaz çifti'nın özelliklerinin kullanılır.

Uzaktan gibi IOT Hub ve cihaz yönetim düzenleri hava bellenim güncelleştirme okuma hello kullanmaya Başlarken toocontinue [Öğreticisi: toodo üretici yazılımı güncelleştirme nasıl][lnk-fwupdate].

IOT Hub ile çalışmaya başlama toocontinue bkz [IOT Edge ile çalışmaya başlama][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
