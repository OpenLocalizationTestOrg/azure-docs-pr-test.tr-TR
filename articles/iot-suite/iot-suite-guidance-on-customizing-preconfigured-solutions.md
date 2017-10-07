---
title: "aaaCustomizing önceden yapılandırılmış çözümleri | Microsoft Docs"
description: "Nasıl toocustomize hello Azure IOT paketi önceden yapılandırılmış çözümler hakkında rehberlik sağlar."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a>Önceden yapılandırılmış bir çözümü özelleştirme

Azure IOT paketi Hello ile sağlanan hello önceden yapılandırılmış çözüm hello suite çalışma birlikte toodeliver bir uçtan uca çözüm içinde hello hizmetlerini gösterme. Bu başlangıç noktasından genişletmek ve belirli senaryolar için hello çözümü özelleştirme çeşitli yerlerde vardır. Aşağıdaki bölümlerde hello bu ortak özelleştirme noktaları açıklar.

## <a name="find-hello-source-code"></a>Merhaba kaynak kod Bul

depoları aşağıdaki hello Github'da Hello kaynak kodu hello önceden yapılandırılmış çözümleri için kullanılabilir:

* Uzaktan izleme: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Tahmine dayalı Bakım: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Bağlı Fabrika: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

toodemonstrate hello desenleri ve uygulamalar tooimplement hello uçtan uca Azure IOT paketi kullanarak bir IOT çözüm işlevselliğini kullanılan hello önceden yapılandırılmış çözümleri için hello kaynak kodu sağlanır. Hakkında daha fazla bilgi bulabilirsiniz toobuild ve hello GitHub depolarının hello çözümlerinde dağıtın.

## <a name="change-hello-preconfigured-rules"></a>Önceden yapılandırılmış hello kuralları Değiştir

Merhaba Uzaktan izleme çözümü üç içeren [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) toohandle cihaz bilgilerini, telemetri ve hello çözümde kuralları mantığı işler.

Merhaba üç analytics iş akışı ve bunların söz dizimi hello derinlemesine açıklanmıştır [Uzaktan izleme çözümünde gezinme önceden yapılandırılmış](iot-suite-remote-monitoring-sample-walkthrough.md). 

Tooalter mantığı hello veya mantığı belirli tooyour senaryo Ekle doğrudan bu işleri düzenleyebilirsiniz. Akış analizi işleri gibi hello bulabilirsiniz:

1. Çok Git[Azure portal](https://portal.azure.com).
2. Toohello kaynak grubuyla aynı IOT çözümü olarak ad hello gidin. 
3. Toomodify istediğiniz hello Azure akış analizi işi seçin. 
4. Seçerek durdurma hello işi **durdurmak** , komutları hello kümesi. 
5. Merhaba giriş, sorgu ve çıkışlarla düzenleyin.
   
    Basit bir değişiklikle toochange hello hello için sorgudur **kuralları** iş toouse bir **"<"** yerine bir **">"**. Merhaba çözüm portalı görüntülenmeye **">"** kullandığınızda, kural düzenleme, ancak iş temel hello toohello değişikliği nedeniyle hello davranışı nasıl çevrilmiş dikkat edin.
6. Merhaba işi Başlat

> [!NOTE]
> Merhaba işleri değiştirme hello Pano toofail neden şekilde hello Uzaktan izleme Panosu belirli verilere, bağlıdır.

## <a name="add-your-own-rules"></a>Kendi kurallarınızı ekleme

Ayrıca Azure akış analizi işi toochanging hello önceden yapılandırılmış, hello Azure portal tooadd yeni işleri kullanın veya yeni sorgular tooexisting işleri ekleyin.

## <a name="customize-devices"></a>Aygıtları özelleştirme

Merhaba en yaygın uzantısı etkinliklerden birini aygıtları belirli tooyour senaryoyla çalışmaktadır. Cihazları ile çalışmak için birkaç yöntem vardır. Bir sanal cihaz toomatch senaryonuz değiştirilmesine veya hello kullanarak bu yöntemleri dahil [IOT cihaz SDK'sı] [ IoT Device SDK] tooconnect fiziksel cihaz toohello çözümünüzü.

Merhaba adım adım kılavuzu tooadding cihazlar için bkz [IOT paketi bağlanan cihazları](iot-suite-connecting-devices.md) makale ve hello [C SDK'sı örneği izleme uzaktan](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Merhaba Uzaktan izleme çözümü ile tasarlanmış toowork örnektir.

### <a name="create-your-own-simulated-device"></a>Sanal cihazınız oluşturma

Hello dahil [Uzaktan izleme çözümünün kaynak kodu](https://github.com/Azure/azure-iot-remote-monitoring), .NET simulator değil. Bu simulator hello bir hello çözüm ve parçası toosend farklı meta veriler, telemetri, alter ve toodifferent komutları ve yöntemleri yanıt olarak sağlanan ' dir.

Merhaba önceden yapılandırılmış Uzaktan izleme çözümü hello benzeticisinde sıcaklık ve nem telemetri yayan için bir cihazın benzetimini yapar. Merhaba hello benzeticisinde değiştirebileceğiniz [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) proje hello GitHub deposunu çatallanmış zaman.

### <a name="available-locations-for-simulated-devices"></a>Sanal cihazlar için kullanılabilir konumları

Merhaba varsayılan konumları kümesidir Seattle/Redmond, Washington, Amerika Birleşik Devletleri. Bu konumları değiştirebilirsiniz [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>İstenen özellik güncelleştirme işleyicisi toohello simulator ekleme

Merhaba çözüm portalında bir aygıt için istenen bir özellik için bir değer ayarlayabilirsiniz. Merhaba aygıt istenen hello özellik değeri aldığında bu hello hello aygıt toohandle hello özellik değişikliği isteğini sorumluluğundadır. bir özellik değeri değişikliği tooadd desteği istenen bir özelliği üzerinden tooadd işleyici toohello simulator gerekir.

Merhaba simulator içeren hello için işleyiciler **SetPointTemp** ve **TelemetryInterval** ayarlayarak güncelleştirebilirsiniz özellikleri istenen hello çözüm portalı değerleri.

Merhaba aşağıdaki örnekte gösterilir hello hello işleyicisi **SetPointTemp** hello özelliğinde istenen **CoolerDevice** sınıfı:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Bu yöntem sıcaklık ve raporları hello geri tooIoT Hub bildirilen özelliği ayarlanarak değiştirmek hello telemetri noktası güncelleştirir.

Örnek önceki hello aşağıdaki hello desende tarafından kendi özelliklerinizi için kendi işleyicilerinizi ekleyebilirsiniz.

Ayrıca hello istenen özellik toohello işleyicisi hello hello örnekten aşağıdaki gösterildiği gibi bağlamanız gerekir **CoolerDevice** Oluşturucusu:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Unutmayın **SetPointTempPropertyName** olan "Config.SetPointTemp" tanımlanan bir sabit.

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Yeni bir yöntem toohello simulator desteği ekleme

Merhaba simulator tooadd desteği için yeni bir özelleştirebilirsiniz [yöntemi (doğrudan yöntemi)][lnk-direct-methods]. Gereken iki temel adımlar verilmiştir:

- Merhaba simulator hello IOT hub'hello yönteminin ayrıntılarla hello önceden yapılandırılmış çözümde bildirmeniz gerekir.
- Merhaba simulator, kod toohandle hello yöntem çağrısı içermelidir, hello çağırdığınızda **cihaz ayrıntıları** Masası hello Çözüm Gezgini'nde ya da bir iş.

Merhaba çözümü kullanan önceden yapılandırılmış Uzaktan izleme *özellikleri bildirilen* desteklenen yöntemleri tooIoT hub toosend ayrıntıları. Merhaba çözüm arka ucu yöntem çağrılarına geçmişini yanı sıra her bir cihaz tarafından desteklenen tüm hello yöntemlerinin listesini tutar. Bu cihazlar hakkındaki bilgileri görüntülemek ve hello çözüm portalı yöntemleri çağırır.

toonotify hello IOT hub, bir aygıt bir yöntem desteklediğini hello aygıt hello yöntemi toohello ayrıntılarını eklemelisiniz **SupportedMethods** hello düğümünde bildirilen özellikleri:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

Merhaba yöntemi imzası olan biçimini izleyen hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Örneğin, toospecify hello **InitiateFirmwareUpdate** yöntemi bekliyor adlı bir dize parametresi **FwPackageURI**, yöntem imzası aşağıdaki hello kullanın:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Merhaba desteklenen parametre türleri listesi için bkz: **CommandTypes** hello altyapısı projesi sınıfta.

toodelete bir yöntem hello yöntemi imza çok ayarlama`null` özellikleri hello bildirdi.

> [!NOTE]
> aldığında hello çözüm arka ucu yalnızca desteklenen yöntemleri hakkında bilgi güncelleştirmeleri bir *aygıt bilgileri* hello aygıttan ileti.

Merhaba hello kod örnekten aşağıdaki **SampleDeviceFactory** hello ortak sınıfında proje gösterir nasıl tooadd yöntemi toohello listesini, **SupportedMethods** hello hello tarafından gönderilen özellikleri bildirdi aygıt:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Bu kod parçacığını hello ayrıntılarını ekler **InitiateFirmwareUpdate** metin toodisplay hello çözüm portalı ve hello ayrıntılarını dahil yöntemi gereken yöntem parametreleri.

Merhaba simulator hello desteklenen yöntemlerin listesi tooIoT hello simulator başladığında Hub içeren bildirilen özelliklerini gönderir.

Onu destekleyen her bir yöntemi için bir işleyici toohello simulator kodu ekleyin. Merhaba varolan işleyicileri hello görebilirsiniz **CoolerDevice** hello Simulator.WebJob projesinde sınıfı. Merhaba aşağıdaki örnekte gösterilir hello işleyicisi **InitiateFirmwareUpdate** yöntemi:

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

Yöntem işleyici adları ile başlamalı `On` ardından hello yöntemi hello adı. Merhaba **methodRequest** parametresi ile Merhaba yöntemi çağırma hello çözüm arka uçtan geçirilen herhangi bir parametre içeriyor. Merhaba dönüş değeri türü olmalıdır **görev&lt;MethodResponse&gt;**. Merhaba **BuildMethodResponse** yardımcı program yöntemi hello dönüş değeri oluşturmanıza yardımcı olur.

Merhaba yöntemi işleyicisinin içinden, olabilir:

- Zaman uyumsuz bir görevi başlatın.
- İstenen özelliklerini hello almak *cihaz çifti* IOT hub.
- Merhaba kullanan tek bildirilen bir özellik güncelleştirme **SetReportedPropertyAsync** hello yönteminde **CoolerDevice** sınıfı.
- Birden çok bildirilen özellikleri oluşturarak güncelleştirmek bir **TwinCollection** örneği ve arama hello **Transport.UpdateReportedPropertiesAsync** yöntemi.

Merhaba bellenim güncelleştirme sabitlerini hello aşağıdaki adımları gerçekleştirir:

- Denetimleri hello mümkün tooaccept hello bellenim güncelleştirme isteği aygıttır.
- Zaman uyumsuz olarak hello bellenim güncelleştirme işlemi başlatır ve hello işlemi tamamlandığında hello telemetri sıfırlar.
- "Kabul FirmwareUpdate" döndürür hello hemen ileti tooindicate hello isteği hello aygıt tarafından kabul edildi.

### <a name="build-and-use-your-own-physical-device"></a>Derleme ve (fiziksel) aygıtınızı kullanın

Merhaba [Azure IOT SDK'ları](https://github.com/Azure/azure-iot-sdks) kitaplıkları çok sayıda aygıt türleri (diller ve işletim sistemleri) bağlamak için IOT çözümleriyle sağlar.

## <a name="modify-dashboard-limits"></a>Pano sınırları değiştirme

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Pano açılır listede görüntülenen aygıt sayısı

Merhaba, 200 varsayılandır. Bu sayıyı değiştirin [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Bing harita denetimindeki PIN'ler toodisplay sayısı

Merhaba, 200 varsayılandır. Bu sayıyı değiştirin [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Süre telemetri grafik

Merhaba varsayılan değer 10 dakikadır. Bu değeri değiştirebilirsiniz [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Uygulama rolleri el ile ayarlamanız

Merhaba aşağıdaki yordamda açıklanmıştır nasıl tooadd **yönetici** ve **ReadOnly** uygulama rolleri tooa önceden yapılandırılmış çözümü. Merhaba azureiotsuite.com sitesinden zaten sağlanan önceden yapılandırılmış çözümler hello içerdiğini **yönetici** ve **ReadOnly** rolleri.

Merhaba üyeleri **ReadOnly** rolü hello Pano ve hello cihaz listesini görebilirsiniz ancak tooadd cihazları, cihaz öznitelikleri Değiştir veya gönderme komutlar izin verilmiyor.  Merhaba üyeleri **yönetici** rolüne sahip tam erişim tooall hello işlevselliği hello çözümde.

1. Toohello Git [Klasik Azure portalı][lnk-classic-portal].
2. **Active Directory**’yi seçin.
3. Çözümünüzü sağlarken, kullanılan hello AAD kiracısını Hello adına tıklayın.
4. **Uygulamalar**'a tıklayın.
5. Merhaba, önceden yapılandırılmış çözümünüzün adıyla eşleşen hello uygulamanın adını tıklatın. Uygulamanızı hello listesinde görmüyorsanız seçin **Şirketimin sahip olduğu uygulamalar** hello içinde **Göster** tıklayın ve açılan hello onay işareti.
6. Merhaba sayfasının Hello altında tıklatın **yönetmek bildirim** ve ardından **karşıdan bildirim**.
7. Bu yordam bir .json dosyası tooyour yerel makine indirir. Tercih ettiğiniz bir metin düzenleyicisinde düzenlemek için bu dosyayı açın.
8. Merhaba üçüncü satıra hello .json dosyası, görebilirsiniz:

   ```json
   "appRoles" : [],
   ```
   Bu satırı koddan hello ile değiştirin:

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. Merhaba güncelleştirilmiş .json dosyası (Merhaba varolan dosyanın üzerine) kaydedin.
10. Merhaba hello sayfanın hello sonundaki Klasik Azure portalı seçin **yönetmek bildirim** sonra **karşıya bildirim** hello önceki adımda kaydettiğiniz tooupload hello .json dosyası.
11. Merhaba şimdi eklediğiniz **yönetici** ve **ReadOnly** rolleri tooyour uygulama.
12. tooassign, dizininizdeki bu rolleri tooa kullanıcı birini bkz [hello azureiotsuite.com sitesindeki izinler][lnk-permissions].

## <a name="feedback"></a>Geri Bildirim

Bu belgede ele alınan toosee istediğiniz özelleştirme var mı? Özellik önerileri çok eklemek[kullanıcı sesi](https://feedback.azure.com/forums/321918-azure-iot), ya da bu makaleye yorum. 

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla hello seçenekleri hello önceden yapılandırılmış çözümleri özelleştirme hakkında toolearn bakın:

* [Mantıksal uygulama tooyour Azure IOT paketi uzaktan önceden yapılandırılmış izleme çözümü bağlantı][lnk-logicapp]
* [Dinamik telemetri hello Uzaktan izleme çözümü ile kullanma][lnk-dynamic]
* [Cihaz bilgi meta verilerde hello Uzaktan izleme çözümü][lnk-devinfo]
* [Merhaba Fabrika çözüm görüntüler veri OPC UA sunucularınızdan nasıl bağlanacağını özelleştirme][lnk-cf-customize]

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md