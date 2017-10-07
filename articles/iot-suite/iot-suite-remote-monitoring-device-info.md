---
title: "meta verilerde hello Uzaktan izleme çözümü aaaDevice bilgi | Microsoft Docs"
description: "Hello Azure IOT önceden yapılandırılmış çözümü uzaktan izlemenin ve mimarisinin açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Cihaz bilgi meta verilerde hello Uzaktan izleme çözümü

Hello Azure IOT paketi Uzaktan izleme çözümü cihaz meta verilerini yönetmek için bir yaklaşım gösterir. Bu makalede hello yaklaşım özetlenmektedir Bu çözüm tooenable alır, toounderstand:

* Hangi cihaz meta verilerini hello çözümü depolar.
* Nasıl hello çözüm hello cihaz meta verilerini yönetir.

## <a name="context"></a>Bağlam

Merhaba çözümü kullanan önceden yapılandırılmış Uzaktan izleme [Azure IOT Hub] [ lnk-iot-hub] tooenable aygıtları toosend veri toohello bulut. Merhaba çözümü üç farklı konumlarda cihazlarla ilgili bilgileri depolar:

| Konum | Depolanan bilgileri | Uygulama |
| -------- | ------------------ | -------------- |
| Kimlik kayıt defteri | Cihaz kimliği, kimlik doğrulaması anahtarları, durumu etkin | Yerleşik tooIoT Hub |
| Cihaz çiftlerini | Meta veriler: bildirilen özellikleri, istenen özellikleri, etiketler | Yerleşik tooIoT Hub |
| Cosmos DB | Komut ve yöntemi geçmişi | Özel çözüm için |

IOT hub'ında bir [cihaz kimlik kayıt defteri] [ lnk-identity-registry] toomanage erişim tooan IOT hub ve kullandığı [cihaz çiftlerini] [ lnk-device-twin] toomanage cihaz meta veriler . Ayrıca bir uzaktan izleme çözümü özgü olan *cihaz kayıt defteri* komutu ve yöntemi geçmişini saklar. Merhaba Uzaktan izleme çözümü kullanan bir [Cosmos DB] [ lnk-docdb] veritabanı tooimplement komut ve yöntemi geçmişi için özel bir depo.

> [!NOTE]
> Uzaktan izleme çözümü Hello hello cihaz kimlik kayıt defteri hello Cosmos DB veritabanında hello bilgilerle eşitlenmiş tutar. Her ikisi de aynı cihaz kimliği toouniquely tanımlamak hello kullan her aygıt bağlı tooyour IOT hub'ı.

## <a name="device-metadata"></a>Cihaz meta veriler

IOT hub'ı tutan bir [cihaz çifti] [ lnk-device-twin] tooa Uzaktan izleme çözümü her sanal ve fiziksel cihaz için bağlı. Merhaba çözüm cihazlarla ilişkilendirilmiş cihaz çiftlerini toomanage hello meta verilerini kullanır. Cihaz çifti IOT Hub tarafından korunan bir JSON belgesinin ve hello çözüm hello IOT Hub API toointeract ile cihaz çiftlerini kullanır.

Cihaz çifti üç tür meta verileri depolar:

- *Özellikler bildirilen* tooan IOT hub cihaz tarafından gönderilir. Hello Uzaktan izleme çözümü, sanal cihazlar bildirilen özellikleri başlatma ve yanıt çok gönderme**cihaz durumunu değiştir** komutlar ve yöntemleri. Hello bildirilen özelliklerini görüntüleyebilirsiniz **cihaz listesi** ve **cihaz ayrıntıları** hello çözüm Portalı'nda. Bildirilen özellikleri salt okunurdur.
- *Özellikler istenen* hello IOT hub'ından cihazlar tarafından alınır. Bunu hello tüm gerekli yapılandırma değiştirme hello aygıtta hello aygıt toomake sorumluluğundadır. Bu ayrıca hello hello aygıt tooreport hello değişikliği geri toohello hub'ı bildirilen bir özellik olarak sorumluluğundadır. İstenen özellik değeri hello çözüm portalı üzerinden ayarlayabilirsiniz.
- *Etiketler* yalnızca hello cihaz çiftine mevcut ve hiçbir zaman bir aygıt ile eşitlenir. Merhaba çözüm portalında etiket değerleri ayarlayın ve cihazların Merhaba listesi filtre bunları kullanın. Merhaba çözüm bir etiket tooidentify hello simgesi toodisplay hello çözüm portalında bir aygıt için de kullanır.

Örnek özellikleri benzetimli hello aygıtlardan üreticisini, model numarası, enlem ve boylam dahil bildirdi. Sanal cihazlar, ayrıca bildirilen bir özellik olarak hello desteklenen yöntemlerin listesi döndürür.

> [!NOTE]
> Merhaba sanal cihaz kodu yalnızca hello kullanan **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** istenen özellikleri tooupdate hello bildirilen geri gönderilen özellikleri tooIoT Hub. Diğer tüm istenen özelliği değişiklik isteklerini göz ardı edilir.

Merhaba aygıt kayıt defteri Cosmos DB veritabanında depolanan bir aygıt bilgileri meta verileri JSON belgesi yapı izlenerek hello sahiptir:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Meta veri toodescribe hello telemetri hello aygıt gönderir tooIoT Hub aygıt bilgileri de içerir. Merhaba Uzaktan izleme çözümü kullanan nasıl hello Pano görüntüler bu telemetri meta veri toocustomize [dinamik telemetri][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Yaşam döngüsü

Merhaba çözüm portalında bir cihaz ilk oluşturduğunuzda, hello çözüm hello Cosmos DB veritabanı toostore komut girişi ve yöntemi Geçmişi oluşturur. Bu noktada, hello çözüm ayrıca hello aygıtı için bir giriş hello anahtarları hello aygıt kullanır tooauthenticate IOT Hub ile oluşturur hello cihaz kimlik kayıt oluşturur. Ayrıca, bir cihaz çifti oluşturur.

Bir cihaz ilk toohello çözüm bağlandığında, bildirilen özellikleri ve bir cihaz bilgi iletisi gönderir. Başlangıç özellik değerlerini otomatik olarak hello cihaz çiftine kaydedilir bildirdi. Merhaba özellikleri hello aygıt üreticisi, model numarası, seri numarası ve desteklenen yöntemlerin listesi dahil bildirdi. Hello cihaz bilgi iletisi hello komut parametreleri hakkında bilgiler dahil olmak üzere hello aygıt destekler hello komutların listesini içerir. Merhaba çözümü bu ileti aldığında, hello Cosmos DB veritabanındaki hello cihaz bilgilerini güncelleştirir.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Aygıt bilgileri hello çözüm portalında görüntüleyin ve düzenleyin

Merhaba hello çözüm portalı aygıt listesinde görüntüler cihaz özellikleri sütunları olarak varsayılan olarak aşağıdaki hello: **durum**, **DeviceID**, **üretici**, **Model numarası**, **seri numarası**, **bellenim**, **Platform**, **İşlemci**ve  **RAM yüklü**. Tıklayarak hello sütunları özelleştirebilirsiniz **sütun düzenleyicisini**. cihaz özellikleri Hello **enlem** ve **boylam** hello Bing harita hello konumda hello Panoda sürücü.

![Aygıt listesinde sütun Düzenleyicisi][img-device-list]

Merhaba, **cihaz ayrıntıları** bölmesinde hello çözüm portalında, istenen özelliklerini ve etiketleri düzenleyebilirsiniz (özellikleri salt okunur bildirilen).

![Cihaz ayrıntıları bölmesi][img-device-edit]

Merhaba çözüm portalı tooremove bir aygıtı çözümünüzden kullanabilirsiniz. Bir aygıt kaldırdığınızda, hello çözüm hello aygıt girişi kimlik kayıt defterinden kaldırır ve hello cihaz çifti siler. Merhaba çözümü, ayrıca bilgi ilgili toohello aygıt hello Cosmos DB veritabanından kaldırır. Bir aygıt kaldırabilmeniz için önce devre dışı bırakmalısınız.

![Aygıt kaldırma][img-device-remove]

## <a name="device-information-message-processing"></a>Cihaz bilgi iletisi işleme

Bir aygıt tarafından gönderilen cihaz bilgileri iletilerini telemetri iletilerini farklıdır. Cihaz bilgileri iletilerini bir cihazın karşılık verebildiği hello komutları ve komut geçmişini içerir. IOT Hub kendisini sahip bir aygıt bilgileri iletideki hello meta verileri olanağıyla ve işlemler hello hello iletisinde aynı şekilde herhangi bir cihaz bulut iletisini işler. Merhaba Uzaktan izleme çözümü, içinde bir [Azure akış analizi] [ lnk-stream-analytics] (ASA) işini IOT Hub'ından karışılama iletileri okur. Merhaba **Deviceınfo** stream analytics iş filtreleri içeren iletileri için **"ObjectType": "Deviceınfo"** ve toohello iletir **EventProcessorHost** ana bilgisayar bir web işi çalıştıktan örneği. Merhaba mantığında **EventProcessorHost** örneği hello cihaz kimliği toofind hello Cosmos DB kayıt hello belirli cihaz ve güncelleştirme hello kayıt için kullanılır.

> [!NOTE]
> Cihaz bilgi iletisi, bir standart cihaz bulut iletisidir. Merhaba çözüm ASA sorguları kullanarak cihaz bilgileri iletilerini ve telemetri iletilerini arasında ayırır.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba önceden yapılandırılmış çözümleri nasıl özelleştirebileceğiniz öğrenme bitirdikten sonra artık hello bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri gözden geçirebilirsiniz:

* [Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]
* [IoT Paketi için sık sorulan sorular][lnk-faq]
* [Merhaba IOT güvenlikten plan][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
