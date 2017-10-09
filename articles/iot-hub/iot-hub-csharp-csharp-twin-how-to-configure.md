---
title: "aaaUse Azure IOT Hub cihaz çifti özellikleri (.NET/.NET) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz tooconfigure cihaz çiftlerini. .NET tooimplement sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sı ve hello .NET tooimplement cihaz çifti kullanarak bir aygıt yapılandırmasını değiştirir bir hizmet uygulaması için Azure IOT hizmeti SDK'sını kullanın."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>İstenen özelliklerde tooconfigure aygıtları'nı kullanın
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Bu öğreticinin Hello sonunda, iki .NET konsol uygulamaları olacaktır:

* **SimulateDeviceConfiguration**, istenen yapılandırma güncelleştirmesi bekler ve benzetimli yapılandırma güncellemeyi hello durumunu raporlar sanal cihaz uygulaması.
* **SetDesiredConfigurationAndQuery**hello ayarlar bir arka uç uygulaması istenen bir cihazda yapılandırma ve sorguları hello yapılandırma güncelleştirme işlemi.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.
> 
> 

toocomplete hello aşağıdaki gereksinim Bu öğretici:

* Visual Studio 2015 veya Visual Studio 2017.
* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.

Merhaba izlediyseniz [cihaz çiftlerini ile çalışmaya başlama] [ lnk-twin-tutorial] öğretici, zaten sahip olduğunuz bir IOT hub ve adlı bir cihaz kimliği **myDeviceId**. Bu durumda, toohello atlayabilirsiniz [oluşturma hello sanal cihaz uygulamasının] [ lnk-how-to-configure-createapp] bölümü.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Merhaba sanal cihaz uygulaması oluşturma
Bu bölümde, tooyour hub olarak bağlanan bir .NET konsol uygulaması oluşturma **myDeviceId**, istenen yapılandırma güncelleştirmesi bekler ve daha sonra güncelleştirmeleri benzetimli hello yapılandırmasını güncelleştirme işlemi raporlar.

1. Visual Studio'da hello kullanarak yeni bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması** proje şablonu. Ad hello proje **SimulateDeviceConfiguration**.
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]

1. Çözüm Gezgini'nde hello sağ **SimulateDeviceConfiguration** proje ve ardından **NuGet paketlerini Yönet...** .
1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**. Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba yer tutucu değerini hello önceki bölümünde belirtildiği hello cihaz bağlantı dizesini değiştirin.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile toointeract duyduğunuz tüm hello yöntemler sunar. Merhaba, yukarıda gösterilen kodu başlatır hello **istemci** nesne ve alır hello cihaz çiftinin **myDeviceId**.

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı. Bu yöntem hello başlangıç değerleri telemetri hello yerel cihazda ayarlar ve ardından güncelleştirmeleri cihaz çifti hello.

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı. Bu değişikliği algılar bir geri çağırma olduğu *özelliklerini istenen* hello cihaz çiftine.

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Bu yöntem güncelleştirmeleri hello bildirilen nesnesindeki özellikleri hello yerel cihaz çifti hello yapılandırmasıyla güncelleştirme isteği ve kümelerini hello durumu çok**bekleyen**, cihaz çifti hello hizmetinde güncelleştirmeleri hello sonra. Merhaba cihaz çifti başarıyla güncelleştirdikten sonra hello yapılandırma değişikliği hello yöntemini çağırarak tamamlanmadan `CompleteConfigChange` hello sonraki noktasında açıklanmaktadır.

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı. Bu yöntem bir cihaz sıfırlama benzetimini yapar, sonra güncelleştirmeleri hello hello durumu çok ayarı yerel bildirilen özellikleri**başarı** ve kaldırır hello **pendingConfig** öğesi. Ardından, hello cihaz çifti hello hizmetinde güncelleştirir. 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Son satırları toohello aşağıdaki hello ekleyin **ana** yöntemi:

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > Bu öğretici herhangi davranışı eşzamanlı yapılandırma güncelleştirmelerini benzetimini değil. Merhaba güncelleştirme çalışırken bazı yapılandırma güncelleştirme işlemleri hedef yapılandırmasının mümkün tooaccommodate değişiklikler olabilir, bazı ve bazı bunları bir hata durumu reddedebilirsiniz tooqueue olabilir. Belirli bir yapılandırma işlemi için istenen davranışı hello ve hello yapılandırma değişikliği başlatmadan önce hello uygun mantığı ekleyin emin tooconsider olun.
   > 
   > 
1. Hello çözümü oluşturmak ve ardından hello cihaz uygulaması tıklayarak Visual Studio'dan çalıştırma **F5**. Merhaba çıkış konsolda sanal cihazınız hello cihaz çifti alma, hello telemetri ayarlama ve istenen özellik değişikliği için bekleyen belirten Merhaba iletileri görmeniz gerekir. Çalışan hello uygulama tutun.

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
   
    Merhaba **kayıt defteri** nesne cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar. Bu kod hello başlatır **kayıt defteri** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve ardından yeni bir telemetri yapılandırma nesnesi ile istenen özelliklerini güncelleştirir.
    Bundan sonra 10 saniyede hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve baskı siparişi hello istenen ve telemetri yapılandırmaları bildirdi. Toohello başvuran [IOT hub'ı sorgu dili] [ lnk-query] nasıl toogenerate zengin raporları, tüm aygıtlarda toolearn.
   
   > [!IMPORTANT]
   > Bu uygulama yalnızca tanım amaçlıdır her 10 saniye IOT hub'ı sorgular. Kullanım toogenerate kullanıcı dönük raporları birçok cihaz ve toodetect değişiklikleri arasında sorgular. Çözümünüz cihaz olayların gerçek zamanlı bildirimler gerektiriyorsa, kullanın [twin bildirimleri][lnk-twin-notifications].
   > 
   > 
1. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **SetDesiredConfigurationAndQuery** projedir **Başlat**. Merhaba çözümü oluşturun.
1. İle **SimulateDeviceConfiguration** cihaz uygulamasının çalışıyor, Visual Studio kullanarak çalışma hello service uygulaması **F5**. Merhaba bildirilen yapılandırma çıkarılıp görmelisiniz **bekleyen** çok**başarı** hello yeni etkin ile 24 saat yerine beş dakikalık sıklığı Gönder.

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
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
