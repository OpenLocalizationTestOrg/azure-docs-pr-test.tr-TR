---
title: "aaaRemote önceden yapılandırılmış izleme çözümünde gezinme | Microsoft Docs"
description: "Hello Azure IOT önceden yapılandırılmış çözümü uzaktan izlemenin ve mimarisinin açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Önceden yapılandırılmış uzaktan izleme çözümünde gezinme

IOT paketi Uzaktan izleme hello [önceden yapılandırılmış çözüm] [ lnk-preconfigured-solutions] olan bir uygulaması, bir uçtan uca izleme çözümünün uzak konumlarda çalışan birden fazla makine için. Merhaba çözüm temel Azure hizmetlerini tooprovide hello iş senaryosunun genel uygulamasını birleştirir. Merhaba çözüm kendi uygulamanız için bir başlangıç noktası olarak kullanabilirsiniz ve [özelleştirme] [ lnk-customize] , toomeet kendi belirli iş gereksinimlerinizi.

Bu makalede bazı temel öğeleri hello Uzaktan izleme çözümü tooenable hello anlatılmaktadır nasıl çalıştığını toounderstand. Bu bilgiler şunları yapmanıza yardımcı olur:

* Merhaba çözümde sorunları giderin.
* Plan nasıl toocustomize toohello çözüm toomeet belirli gereksinimlerinizi. 
* Azure hizmetlerini kullanan kendi IoT çözümünüzü tasarlama.

## <a name="logical-architecture"></a>Mantıksal mimari

Diyagram aşağıdaki hello hello hello önceden yapılandırılmış çözümün mantıksal bileşenlerinin ana hatların vermektedir:

![Mantıksal mimari](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Sanal cihazlar

Merhaba önceden yapılandırılmış çözümde hello sanal cihaz bir soğutma aygıtı (örneğin, bir yapının klimaları veya tesisin havalandırma birimi) temsil eder. Merhaba önceden yapılandırılmış çözümü dağıttığınızda, Çalıştır dört sanal cihaz da otomatik olarak sağlamak bir [Azure WebJob][lnk-webjobs]. Benzetimli hello aygıtlar, tooexplore hello davranışı hello gerek toodeploy olmadan hello çözümün herhangi bir fiziksel cihaza kolaylaştırır. toodeploy gerçek fiziksel bir aygıtı Bkz hello [Uzaktan izleme çözümü, aygıt toohello bağlanmak] [ lnk-connect-rm] Öğreticisi.

### <a name="device-to-cloud-messages"></a>Cihazdan buluta iletiler

Her sanal cihaz ileti türleri tooIoT Hub aşağıdaki hello gönderebilirsiniz:

| İleti | Açıklama |
| --- | --- |
| Başlangıç |Merhaba cihaz başlatıldığında, gönderen bir **cihaz bilgileri** toohello arka uç kendi hakkında bilgileri içeren ileti. Cihazın desteklediği yöntemleri hello ve bu verileri hello cihaz kimliği ve hello komutların listesini içerir. |
| Varlık |Bir aygıt düzenli aralıklarla gönderir bir **varlığı** hello aygıt algılayıcı hello varlığını algılayabilir olup olmadığını tooreport iletisi. |
| Telemetri |Bir aygıt düzenli aralıklarla gönderir bir **telemetri** hello sıcaklık ve nem hello aygıttan toplanan sanal değerlerini bildiren bir ileti algılayıcılar benzetimli. |

> [!NOTE]
> Merhaba çözüm hello aygıt Cosmos DB veritabanında alan ve hello cihaz çifti tarafından desteklenen komutları hello listesini depolar.

### <a name="properties-and-device-twins"></a>Özellikler ve cihaz ikizleri

Merhaba sanal cihazlar Gönder cihaz özellikleri toohello aşağıdaki hello [twin] [ lnk-device-twins] hello IOT hub ' *özellikleri bildirilen*. Merhaba aygıt gönderir bildirilen özellikleri başlangıçta ve yanıt tooa **cihaz durumunu değiştir** komut veya yöntemi.

| Özellik | Amaç |
| --- | --- |
| Config.TelemetryInterval | Sıklık (saniye) hello cihaz telemetri gönderir |
| Config.TemperatureMeanValue | Merhaba benzetimli sıcaklık telemetri Hello ortalama değerini belirtir |
| Device.DeviceID |Sağlanan veya bir aygıt hello çözümde oluşturulduğunda atanan kimliği |
| Device.DeviceState | Merhaba aygıt tarafından bildirilen durum |
| Device.CreatedTime |Zaman hello aygıt hello çözümde oluşturuldu |
| Device.StartupTime |Zaman hello aygıt başlatıldı. |
| Device.LastDesiredPropertyChange |Merhaba son istenen özelliği Hello sürüm numarasını değiştirme |
| Device.Location.Latitude |Merhaba cihazın enlem konumu |
| Device.Location.Longitude |Merhaba cihazın boylam konumu |
| System.Manufacturer |Cihaz üreticisi |
| System.ModelNumber |Merhaba cihazın model numarası |
| System.SerialNumber |Merhaba cihaz seri numarası |
| System.FirmwareVersion |Geçerli hello cihazdaki üretici yazılımı sürümü |
| System.Platform |Merhaba cihazın Platform mimarisi |
| System.Processor |İşlemci çalışan hello aygıtı |
| System.InstalledRAM |Merhaba cihazda yüklü RAM miktarı |

Merhaba benzetici, örnek değerlerle sanal cihazlarda bu özelliklerin çekirdeğini oluşturur. Merhaba simulator başlatır sanal cihaz, hello cihaz her zaman hello önceden tanımlanmış meta verileri tooIoT Hub bildirilen özellikleri olarak bildirir. Bildirilen özellikleri yalnızca hello aygıt tarafından güncelleştirilebilir. toochange bildirilen bir özellik, çözüm Portalı'nda istenen bir özellik Ayarla. Merhaba cihaza hello sorumluluğunda olan:

1. Düzenli aralıklarla istenen hello IOT hub'ından alınamıyor.
2. İstenen başlangıç özellik değeri ile yapılandırmasını güncelleştirin.
3. Merhaba yeni değer geri toohello hub'ı bildirilen bir özellik olarak gönderin.

Merhaba çözüm panodan kullandığınız *özellikleri istenen* tooset özellikleri hello kullanarak bir cihazdaki [cihaz çifti][lnk-device-twins]. Genellikle, bir cihaz hello hub tooupdate kendi iç durumu ve rapor hello geri bildirilen bir özellik olarak değiştirmek istediğiniz özellik değeri okur.

> [!NOTE]
> Merhaba sanal cihaz kodu yalnızca hello kullanan **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** istenen özellikleri tooupdate hello bildirilen geri gönderilen özellikleri tooIoT Hub. Diğer tüm istenen özelliği değişiklik isteklerini hello sanal cihazda göz ardı edilir.

### <a name="methods"></a>Yöntemler

Merhaba sanal cihazlar yöntemler aşağıdaki hello işleyebilir ([doğrudan yöntemleri][lnk-direct-methods]) hello çözüm portalı hello IOT hub'ı aracılığıyla çağrılır:

| Yöntem | Açıklama |
| --- | --- |
| InitiateFirmwareUpdate |Merhaba aygıt tooperform bellenim güncelleştirme yönlendirir |
| Yeniden başlatma |Merhaba aygıt tooreboot bildirir |
| FactoryReset |Bir fabrika ayarlarına sıfırlayıp hello aygıt tooperform bildirir |

Bazı yöntemler bildirilen özellikleri tooreport ilerlemeyi kullanın. Örneğin, hello **InitiateFirmwareUpdate** yöntemi zaman uyumsuz olarak hello cihazda çalışan hello güncelleştirme benzetimini yapar. Merhaba zaman uyumsuz görev geri toosend durum güncelleştirmeleri devam ederken hello yöntemi hemen hello aygıtta döndürür toohello çözüm panosunu kullanma özellikleri bildirdi.

### <a name="commands"></a>Komutlar

Benzetimli hello cihazlar hello çözüm portalı hello IOT hub'ı aracılığıyla gönderilen komutları (bulut-cihaz iletilerini) aşağıdaki hello işleyebilir:

| Komut | Açıklama |
| --- | --- |
| PingDevice |Gönderen bir *ping* Canlı toohello aygıt toocheck |
| StartTelemetry |Telemetri göndermesini başlatır hello cihaz |
| StopTelemetry |Cihazın telemetri göndermesini durdurur hello |
| ChangeSetPointTemp |Değişiklikleri hello ayar noktası değerini hangi hello rastgele verilerin oluşturulur |
| DiagnosticTelemetry |Aygıt benzeticisi toosend ek bir telemetri değeri (externalTemp) Tetikleyicileri hello |
| ChangeDeviceState |Merhaba cihaz için Genişletilmiş durum özelliğini değiştirir ve hello aygıttan hello cihaz bilgi iletisi gönderir |

> [!NOTE]
> Bu komutlar (buluttan cihaza iletiler) ile yöntemlerin (doğrudan yöntemler) bir karşılaştırması için bkz. [Buluttan cihaza iletişim kılavuzu][lnk-c2d-guidance].

## <a name="iot-hub"></a>IoT Hub’ı

Merhaba [IOT hub'ı] [ lnk-iothub] hello aygıtlardan hello buluta gönderilen verileri alır ve kullanılabilir toohello Azure Stream Analytics (ASA) işini kolaylaştırır. Her akış ASA işi cihazlarınızdan gelen iletileri ayrı IOT Hub tüketici grubu tooread hello akışı kullanır.

IOT hub'hello çözümde de hello:

- Merhaba kimlikleri ve tooconnect toohello portal izin verilen tüm hello cihazların kimlik doğrulama anahtarlarını depolayan bir kimlik kayıt defteri tutar. Etkinleştirme ve cihazları hello kimlik kayıt defteri aracılığıyla devre dışı bırakabilirsiniz.
- Komutları tooyour cihazların Merhaba çözüm portalı adına gönderir.
- Merhaba çözüm portalı adına cihazlarınızda yöntemleri çağırır.
- Tüm kayıtlı cihazlar için cihaz ikizlerini tutar. Cihaz çifti bir cihaz tarafından raporlanan hello özellik değerlerini depolar. Cihaz çifti hello çözüm portalında, sonraki bağlandığında hello aygıt tooretrieve ayarlamak istediğiniz özellikleri de depolar.
- Zamanlamaları birden çok aygıt tooset özelliklerini işleri veya birden çok aygıta yöntemleri çağırma.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

Uzaktan izleme çözümü, hello içinde [Azure akış analizi] [ lnk-asa] (ASA) işleme veya depolama hello IOT hub tooother arka uç bileşenleri tarafından alınan aygıt iletileri gönderir. Farklı ASA işleri Merhaba iletileri Merhaba içeriğine göre belirli işlevler gerçekleştirir.

**İş 1: Cihaz bilgileri** hello gelen ileti akışından cihaz bilgileri iletilerine filtre uygular ve bunları tooan olay hub'ı uç gönderir. Bir aygıt cihaz bilgileri iletilerini başlangıçta ve yanıt tooa gönderir **Senddeviceınfo** komutu. Bu iş şu Sorgu tanımını tooidentify hello kullanır **cihaz bilgileri** iletileri:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

Bu iş daha ayrıntılı işleme için kendi çıktı tooan olay hub'ı gönderir.

**İş 2: Kurallar** cihaz başına eşiklere karşılık gelen sıcaklık ve nem telemetrisi değerlerini değerlendirir. Eşik değerleri hello çözüm portalında kullanılabilir hello kurallar düzenleyicisinde ayarlanır. Her cihaz/değer çifti, Akış Analizi’nin **Başvuru Verileri** olarak okuduğu blob’daki zaman damgası tarafından depolanır. Merhaba iş herhangi boş olmayan değerleri hello hello cihaz için ayarlanan eşikle karşılaştırır. Merhaba aşarsa, ' >' koşulunu, hello iş bir **alarm** bu hello eşik gösteren olay aşılırsa ve hello cihaz, değer ve zaman damgası değerlerini sağlar. Bu iş bir alarm tetiklemesi gereken sorgu tanımı tooidentify telemetri iletilerini aşağıdaki hello kullanır:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Merhaba iş kendi çıktı tooan olay hub'ı başka bir işleme için gönderir ve hello çözüm portalı hello uyarı bilgilerini nerede okuyabileceği her uyarı tooblob depolama ayrıntılarını kaydeder.

**Ş 3: Telemetri** hello gelen cihaz telemetrisi akışını iki yolla çalıştırır. Merhaba önce hello aygıtları toopersistent blob depolamadan uzun vadeli depolama için tüm telemetri iletilerini gönderir. Merhaba, ortalama, minimum ve Maksimum nem beş dakikalık kayan pencere üzerinde değerleri ve bu verileri tooblob depolama gönderir ikinci hesaplar. Merhaba çözüm portalı blob depolama toopopulate hello grafikten hello telemetri verilerini okur. Bu iş hello aşağıdaki sorgu tanımını kullanır:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Event Hubs

Merhaba **cihaz bilgileri** ve **kuralları** ASA işleri çıktı kendi veri tooEvent hub tooreliably İleri toohello üzerinde **olay işlemcisi** hello Web işi çalışıyor.

## <a name="azure-storage"></a>Azure Storage

Merhaba çözüm Azure blob depolama toopersist hello çözümde hello aygıtlardan tüm hello ham ve Özet telemetri verilerini kullanır. Merhaba portal blob depolama toopopulate hello grafikten hello telemetri verilerini okur. telemetri aşıldı değerleri hello eşik değerleri yapılandırıldığında toodisplay uyarıları kaydeden blob depolama alanından hello veri hello çözüm portalı okur. Merhaba çözüm ayrıca hello çözüm portalında ayarladığınız blob depolama toorecord hello eşik değerleri kullanır.

## <a name="webjobs"></a>WebJobs

Ayrıca toohosting hello cihaz benzeticilerini hello WebJobs hello çözümde de konak hello **olay işlemcisi** komut yanıtlarını işleyen bir Azure WebJob içinde çalışan. Komut yanıtı iletileri tooupdate hello cihaz komut geçmişini (Merhaba Cosmos DB veritabanında depolanır) kullanır.

## <a name="cosmos-db"></a>Cosmos DB

Merhaba çözüm hello aygıtları bağlı toohello çözüm Cosmos DB veritabanı toostore bilgilerini kullanır. Bu bilgiler hello geçmişi hello çözüm Portalı'ndan toodevices gönderilen komutları ve hello çözüm Portalı'ndan çağrılan yöntemler içerir.

## <a name="solution-portal"></a>Çözüm portalı

Merhaba çözüm portalı hello önceden yapılandırılmış çözümün bir parçası dağıtılan bir web uygulamasıdır. Merhaba anahtar hello çözüm portalında hello Pano ve hello cihaz listesi sayfalarıdır.

### <a name="dashboard"></a>Pano

Merhaba web uygulamasındaki bu sayfa Powerbı javascript denetimlerini kullanır (bkz [Powerbı-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) hello cihazlardan toovisualize hello telemetri verileri. Merhaba çözüm hello ASA telemetri işini toowrite hello telemetri verileri tooblob depolama kullanır.

### <a name="device-list"></a>Cihaz listesi

Bu sayfadan hello çözüm portalında şunları yapabilirsiniz:

* Yeni bir cihaz hazırlayın. Bu eylemin hello benzersiz cihaz kimliğini ayarlar ve hello kimlik doğrulama anahtarı oluşturur. Merhaba çözüme özel Cosmos DB veritabanı ve hello aygıt tooboth hello IOT Hub kimlik kayıt defteri hakkında bilgi yazar.
* Cihaz özelliklerini yönetin. Bu eylem, mevcut özellikleri görüntülemeyi ve yeni özelliklerle güncelleştirmeyi kapsar.
* Komutları tooa aygıt gönderin.
* Bir aygıt için Hello komut geçmişini görüntüleme.
* Cihazları etkinleştirin ve devre dışı bırakın.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba aşağıdaki TechNet blog gönderileri hello Uzaktan izleme çözümü hakkında daha ayrıntılı bilgi sağlar:

* [IOT paketi - altında hello başlık - Uzaktan izleme](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT Paketi - Uzaktan İzleme - Canlı ve Sanal Cihaz Ekleme](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

Makaleler hello okuyarak IOT paketi ile çalışmaya başlayabilirsiniz:

* [Uzaktan izleme çözümü, aygıt toohello Bağlan][lnk-connect-rm]
* [Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
