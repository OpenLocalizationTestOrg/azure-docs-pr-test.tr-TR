---
title: "aaaGet başlatılan Azure IOT Hub cihaz çiftlerini (.NET/.NET) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz çiftlerini tooadd etiketleri ve IOT Hub sorgusuyla kullanın. .NET tooimplement hello sanal cihaz uygulamasının ve hello .NET tooimplement hello etiketleri ekler ve hello IOT hub'ı sorgu çalışan bir hizmet uygulaması için Azure IOT hizmeti SDK'sı için hello Azure IOT cihaz SDK'sını kullanın."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a>Cihaz çiftlerini (.NET/.NET) ile çalışmaya başlama
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Bu öğreticinin Hello sonunda, bu .NET konsol uygulamaları olacaktır:

* **CreateDeviceIdentity**, bir cihaz kimliği ve ilişkili güvenlik oluşturan bir .NET uygulaması, sanal cihaz uygulamasının tooconnect anahtar.
* **AddTagsAndQuery**, etiketleri ekler ve cihaz çiftlerini sorgular .NET arka uç uygulaması.
* **ReportConnectivity**, bir cihaza benzetim yapan tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve kendi bağlantı koşulu raporları .NET cihaz uygulaması.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.
> 
> 

toocomplete hello aşağıdaki gereksinim Bu öğretici:

* Visual Studio 2015 veya Visual Studio 2017.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Toocreate hello cihaz kimliği programlı olarak bunun yerine isterseniz, hello hello ilgili bölümünü okuyun [.NET kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanmak] [ lnk-device-identity-csharp] makalesi.

## <a name="create-hello-service-app"></a>Merhaba service uygulaması oluşturma
Bu bölümde, konum meta veri toohello cihaz çifti ile ilişkili ekler (C# kullanarak) bir .NET konsol uygulaması oluşturma **myDeviceId**. Ardından hello cihaz çiftlerini hello IOT hub'ı hello bulunan hello aygıtları seçerek BİZE depolanır ve bir cep telefonu bağlantı bildirilen olanları hello sorgular.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Ad hello proje **AddTagsAndQuery**.
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. Çözüm Gezgini'nde hello sağ **AddTagsAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .
1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices**. Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices;
1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Merhaba **RegistryManager** sınıfı cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar. Merhaba önceki kod ilk hello başlatır **registryManager** nesnesi alır cihaz çiftinin hello sonra **myDeviceId**ve son olarak, etiketleri istenen hello konumu bilgilerle güncelleştirir.
   
    Güncelleştirdikten sonra iki sorguları yürüten: hello ilk yalnızca hello cihaz çiftlerini hello bulunan aygıtların seçer **Redmond43** tesis ve ayrıca üzerinden bağlanan hello ikinci iyileştirir hello sorgu tooselect yalnızca hello cihazları cep telefonu şebekesi.
   
    Merhaba oluşturduğunda bu hello önceki kod Not **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir. Merhaba **sorgu** nesnesini içeren bir **HasMoreResults** tooinvoke hello kullanabileceğiniz boolean özelliği **GetNextAsTwinAsync** yöntemleri birden çok kez tooretrieve tüm sonuçları. Bir yöntem olarak adlandırılan **GetNextAsJson** değil cihaz çiftlerini, örneğin, sonuçları için toplama sorguların sonuçlarını kullanılabilir.
1. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **AddTagsAndQuery** projedir **Başlat**. Merhaba çözümü oluşturun.
1. Merhaba üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **AddTagsAndQuery** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**. Bulunan tüm cihazlar için sorgu hello soran bir cihazda hello sonuçlarında görmelisiniz **Redmond43** ve hiçbiri hello kısıtlayan hello sorgu için bir cep telefonu şebekesi kullanmak toodevices sonuçlanır.
   
    ![Sorgu Sonuçları penceresinde][img-addtagapp]

Hello sonraki bölümdeki hello bağlantı bilgilerini raporları bir cihaz uygulaması oluşturma ve değişiklikleri hello önceki bölümdeki hello sorgusunun sonucu hello.

## <a name="create-hello-device-app"></a>Merhaba cihaz uygulaması oluşturma
Bu bölümde, tooyour hub olarak bağlanan bir .NET konsol uygulaması oluşturma **myDeviceId**ve ardından, bir cep telefonu şebekesi kullanarak bağlı olduğu bildirilen özellikleri toocontain hello bilgilerini güncelleştirir.

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu. Ad hello proje **ReportConnectivity**.
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]
    
1. Çözüm Gezgini'nde hello sağ **ReportConnectivity** proje ve ardından **NuGet paketlerini Yönet...** .
1. Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**. Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin. Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Aşağıdaki alanları toohello hello eklemek **Program** sınıfı. Merhaba yer tutucu değerini hello önceki bölümünde belirtildiği hello cihaz bağlantı dizesini değiştirin.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile toointeract duyduğunuz tüm hello yöntemler sunar. Merhaba, yukarıda gösterilen kodu başlatır hello **istemci** nesne ve alır hello cihaz çiftinin **myDeviceId**.

1. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   Merhaba güncelleştirmeleri yukarıdaki kodu **myDeviceId**hello bağlantı bilgilerini özelliğiyle bildirilen.

1. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **ReportConnectivity** projedir **Başlat**. Merhaba çözümü oluşturun.
1. Merhaba üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **ReportConnectivity** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**. Merhaba twin bilgi alma ve bağlantı olarak gönderme görmelisiniz bir *özelliği bildirilen*.
   
    ![Cihaz uygulama tooreport bağlantısı çalıştırın][img-rundeviceapp]
    
    
1. Merhaba aygıt bildirilen bağlantı bilgilerini, her iki sorgularda görüntülenmelidir. Merhaba .NET çalıştırmak **AddTagsAndQuery** uygulama toorun hello yeniden sorgular. Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.
   
    ![Başarıyla bildirilen cihaz bağlantısı][img-tagappsuccess]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve bir sanal cihaz uygulaması tooreport aygıt bağlantı bilgilerini hello cihaz çiftine yazıldı. Ayrıca nasıl öğrenilen tooquery hello SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri.

Kaynakları toolearn nasıl aşağıdaki kullanım hello için:

* Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici
* cihaz çifti'nın istenen özellikleri ile hello kullanarak cihazları yapılandırma [kullanım istenen özellikleri tooconfigure aygıtları] [ lnk-twin-how-to-configure] öğretici,
* Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

