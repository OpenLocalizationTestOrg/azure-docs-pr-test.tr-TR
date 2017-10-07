---
title: "aaaAzure IOT önceden yapılandırılmış çözümleri | Microsoft Docs"
description: "Önceden yapılandırılmış çözümleri ve mimarilerini bağlantılar tooadditional kaynaklarla hello Azure IOT bir açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Hello Azure IOT paketi önceden yapılandırılmış çözümleri nelerdir?

Hello Azure IOT paketi önceden yapılandırılmış çözümleri, aboneliği kullanarak tooAzure dağıtabilirsiniz yaygın IOT çözüm modellerinin uygulamalarıdır. Merhaba önceden yapılandırılmış çözümleri kullanabilirsiniz:

* Kendi IoT çözümleriniz için bir başlangıç noktası olarak.
* IOT çözüm tasarımı ve geliştirmesinde ortak yaklaşımlar hakkında toolearn.

Önceden yapılandırılmış her çözüm kullandığı cihazları toogenerate telemetri benzetimli bir tam, uçtan uca uygulamasıdır.

Merhaba tam kaynak kodu toocustomize indirin ve size özel IOT gereksinimlerini hello çözüm toomeet genişletir.

> [!NOTE]
> Merhaba, toodeploy önceden yapılandırılmış çözümleri, ziyaret [Microsoft Azure IOT paketi][lnk-azureiotsuite]. Merhaba makale [hello IOT önceden yapılandırılmış çözümleri kullanmaya başlama] [ lnk-getstarted-preconfigured] nasıl toodeploy ve çalışma birini çözümleri hello hakkında daha fazla bilgi sağlar.

Merhaba aşağıdaki tabloda hello çözümleri toospecific IOT özelliklerini nasıl eşleme gösterilmektedir:

| Çözüm | Veri alımı | Cihaz kimliği | Cihaz yönetimi | Komut ve denetim | Kurallar ve eylemler | Tahmine dayalı analiz |
| --- | --- | --- | --- | --- | --- | --- |
| [Uzaktan izleme][lnk-getstarted-preconfigured] |Evet |Evet |Evet |Evet |Evet |- |
| [Tahmine dayalı bakım][lnk-predictive-maintenance] |Evet |Evet |- |Evet |Evet |Evet |
| [Bağlı fabrika][lnk-getstarted-factory] |Evet |Evet |Evet |Evet |Evet |- |

* *Veri alımı*: ölçek toohello bulut adresindeki veri.
* *Cihaz kimliği*: benzersiz cihaz kimlikleri yönetmek ve denetlemek aygıt erişim toohello çözümü.
* *Cihaz yönetimi*: Cihaz meta verilerini yönetin ve cihazı yeniden başlatma ile üretici yazılımını yükseltme gibi işlemleri gerçekleştirin.
* *Komut ve Denetim*: toocause hello aygıt tootake bir eylem, iletileri tooa aygıt hello buluttan gönderin.
* *Kurallar ve Eylemler*: tooact belirli cihaz bulut verilerini, hello çözüm arka ucu kuralları kullanır.
* *Tahmine dayalı analiz*: hello çözüm arka ucu belirli eylemleri gerçekleşeceğini, cihaz bulut veri toopredict analiz eder. Örneğin, motor bakımının son olduğunda uçak motoru telemetri toodetermine çözümleniyor.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>Önceden yapılandırılmış Uzaktan İzleme çözümüne genel bakış

Biz, diğer çözümleri paylaşımı hello çok sayıda ortak tasarım öğesi gösterdiğinden, bu makalede önceden yapılandırılmış Uzaktan izleme çözümü toodiscuss hello seçtiniz.

Merhaba Aşağıdaki diyagram Uzaktan izleme çözümü hello hello temel öğeleri gösterir. Merhaba aşağıdaki bölümlerde bu öğeler hakkında daha fazla bilgi sağlar.

![Önceden yapılandırılmış Uzaktan İzleme çözümü mimarisi][img-remote-monitoring-arch]

## <a name="devices"></a>Cihazlar

Merhaba Uzaktan izleme çözümü dağıttığınızda, dört sanal cihaz bir soğutma cihazının benzetimini hello çözümde önceden hazırlanır. Bu sanal cihazlarda telemetri yayan yerleşik bir sıcaklık ve nem modeline bulunur. Bu sanal cihazlar aşağıdaki amaçlar için dahil edilir:

- Veri hello çözüm aracılığıyla uçtan uca akışını Hello gösterilmektedir.
- Kullanışlı bir telemetri kaynağı sağlamak.
- Arka uç geliştiriciyseniz hello çözüm için özel bir uygulama bir başlangıç noktası olarak kullanarak bir hedef yöntemleri veya komutları sağlayın.

Benzetimli hello cihazları hello çözümüne bulut-cihaz iletişimi aşağıdaki toohello yanıt verebilir:

- *Yöntemler ([doğrudan yöntemleri][lnk-direct-methods])*: bağlı bir aygıt olduğu beklenen toorespond hemen bir iki yönlü iletişim yöntemi.
- *Komutları (bulut-cihaz iletilerini)*: Burada bir aygıtı alır hello komutu dayanıklı sıradan bir tek yönlü iletişim yöntemi.

Bu farklı yaklaşımların bir karşılaştırması için bkz. [Buluttan cihaza iletişim kılavuzu][lnk-c2d-guidance].

Bir cihaz ilk tooIoT Hub hello önceden yapılandırılmış çözümde bağlandığında, bir cihaz bilgi iletisi toohello hub gönderir. Bu ileti hello cihazın karşılık verebildiği hello yöntemlerini numaralandırır. Hello Uzaktan izleme çözümü, bu yöntemleri sanal cihazları destekler:

* *Bellenim güncelleştirme başlatmak*: Bu yöntem hello aygıt tooperform bellenim güncelleştirme zaman uyumsuz bir görev başlatır. Merhaba zaman uyumsuz görev bildirilen özellikleri toodeliver durum güncelleştirmeleri toohello çözüm Panosu kullanır.
* *Yeniden başlatma*: Bu yöntem benzetimli hello aygıt tooreboot neden olur.
* *FactoryReset*: Bu yöntem hello sanal cihazda bir Fabrika sıfırlaması tetikler.

Bir cihaz ilk tooIoT Hub hello önceden yapılandırılmış çözümde bağlandığında, bir cihaz bilgi iletisi toohello hub gönderir. Bu ileti hello cihazın karşılık verebildiği hello komutları numaralandırır. Hello Uzaktan izleme çözümü, bu komutları sanal cihazları destekler:

* *Ping aygıt*: hello aygıt toothis komutu bir bildirimle yanıtlar. Bu komut, hello cihazın halen etkin ve dinleniyor denetlemek için kullanışlıdır.
* *Telemetriyi Başlat*: telemetri göndermesini hello aygıt toostart bildirir.
* *Telemetriyi Durdur*: telemetri göndermesini hello aygıt toostop bildirir.
* *Sıcaklık ayar noktasını Değiştir*: denetimleri hello benzetimli sıcaklık telemetri değerlerini hello cihaz gönderir. Bu komut, arka uç mantığının test edilmesi için yararlıdır.
* *Telemetriyi*: hello aygıt hello dış sıcaklığı telemetri olarak gönderip göndermediğini denetler.
* *Cihaz durumunu değiştir*: cihaz raporları hello hello cihaz durumu meta veri özelliğini ayarlar. Bu komut, arka uç mantığının test edilmesi için yararlıdır.

Merhaba yayma daha fazla sanal cihazlar toohello çözüm ekleyebilirsiniz aynı telemetri ve yanıt toohello aynı yöntemleri ve komutları.

Ayrıca tooresponding toocommands ve yöntemleri, hello çözümü kullanan [cihaz çiftlerini][lnk-device-twin]. Cihazlar cihaz çiftlerini tooreport özellik değerleri toohello çözüm arka ucu kullanır. Merhaba çözüm Panosu cihazlarda cihaz çiftlerini tooset istenen toonew özellik değerlerini kullanır. Örneğin, hello bellenim güncelleştirme işlemi benzetimli hello cihaz raporları sırasında hello hello durumunu güncelleştirmek bildirilen özelliklerini kullanma.

## <a name="iot-hub"></a>IoT Hub’ı

Önceden yapılandırılmış bu çözümde hello IOT Hub örneği toohello karşılık gelen *bulut ağ geçidi* tipik bir [IOT çözüm mimarisi][lnk-what-is-azure-iot].

IOT hub'ı telemetriyi tek uç noktada hello aygıtlardan alır. IOT hub'ı her aygıt tooit gönderilen hello komutları burada alabilir cihaza özel uç noktaları da korur.

Merhaba IOT hub'ı hello alınan telemetri hello Hizmet tarafı telemetri okuma uç noktasında yoluyla kullanılabilir hale getirir.

IOT Hub'ının Hello cihaz yönetim yeteneği, toomanage gibi işlemleri gerçekleştirmek hello çözüm portalı ve zamanlama işleri, cihaz özelliklerini sağlar:

- Cihazları yeniden başlatma
- Cihaz durumlarını değiştirme
- Üretici yazılımı güncelleştirmeleri

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

Merhaba önceden yapılandırılmış çözümü üç kullanan [Azure akış analizi] [ lnk-asa] (ASA) işleri toofilter hello telemetri akışına hello aygıtları:

* *Deviceınfo işi* -cihaz kayıt özgü iletilerin toohello çözüm cihazı kayıt defterine yönlendiren çıkışları veri tooan olay hub'ı. Bu cihaz kayıt defteri bir Azure Cosmos DB veritabanıdır. Bu iletiler bir cihaz ilk kez bağlandığında veya yanıt tooa gönderilir **cihaz durumunu değiştir** komutu.
* *Telemetry işi* - soğuk depolama için tüm ham telemetri tooAzure blob depolama gönderir ve hello çözüm panosunda görüntülenen telemetri toplamalarını hesaplar.
* *Rules işi* - filtreleri hello kural eşiklerini aşan değerleri telemetri akışına ve çıkışları hello veri tooan olay hub'ı. Bir kural başlatıldığında hello çözüm portalı Panosu görünümü bu olayı hello alarm geçmişi tablosunun yeni bir satır olarak görüntüler. Bu kurallar eylemin hello üzerinde tanımlı hello ayarlara göre de tetikleyebilirsiniz **kuralları** ve **Eylemler** hello çözüm portalı görünümlerde.

Önceden yapılandırılmış bu çözümde toohello parçasını hello ASA işleri **IOT çözümü arka ucu** tipik bir [IOT çözüm mimarisi][lnk-what-is-azure-iot].

## <a name="event-processor"></a>Olay işlemcisi

Önceden yapılandırılmış bu çözümde hello olay işlemcisi forms hello parçası **IOT çözümü arka ucu** tipik bir [IOT çözüm mimarisi][lnk-what-is-azure-iot].

Merhaba **Deviceınfo** ve **kuralları** ASA işleri tooother arka uç hizmetlerinin kendi çıktı tooEvent hub'ları teslimat için Gönder. Merhaba çözümü kullanan bir [EventProcessorHost] [ lnk-event-processor] örnek, çalışır durumda bir [WebJob][lnk-web-job], tooread hello iletileri bu olay hub '. Merhaba **EventProcessorHost** kullanır:
- Merhaba **Deviceınfo** hello Cosmos DB veritabanındaki verileri tooupdate hello cihaz verileri.
- Merhaba **kuralları** veri tooinvoke hello mantığı uygulama ve güncelleştirme hello Uyarıları görüntüle hello çözüm Portalı'nda.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>Cihaz kimliği kayıt defteri, cihaz ikizi ve Cosmos DB

Her IoT hub'ında cihaz anahtarlarını depolayan bir [cihaz kimliği kayıt defteri][lnk-identity-registry] vardır. IOT hub'ı kullanan bu bilgileri cihazların kimliğini doğrulamak - bir cihazı kayıtlı olması gerekir ve toohello hub'a bağlanmadan önce geçerli bir anahtara sahip.

A [cihaz çifti] [ lnk-device-twin] hello IOT Hub tarafından yönetilen bir JSON belge. Bir cihazın cihaz ikizi şunları içerir:

- Merhaba aygıt toohello hub tarafından gönderilen bildirilen özellikler. Bu özellikleri hello çözüm Portalı'nda görüntüleyebilirsiniz.
- İstenen özellikler toosend toohello aygıt istiyor. Bu özellikleri hello çözüm Portalı'nda ayarlayabilirsiniz.
- Yalnızca hello cihaz çifti ve hello cihazda mevcut etiketler. Bu etiketler toofilter listeler cihazların Merhaba çözüm portalında kullanabilirsiniz.

Bu çözüm cihaz çiftlerini toomanage cihaz meta verilerini kullanır. Merhaba çözüm ayrıca her cihaz ve hello komut geçmişini tarafından desteklenen hello komutları gibi Cosmos DB veritabanı toostore ek çözüme özel aygıt verilerini kullanır.

Merhaba çözüm ayrıca hello hello Cosmos DB veritabanı içeriğiyle eşitlenmiş hello cihaz kimliği kayıt defterindeki hello bilgileri tutmanız gerekir. Merhaba **EventProcessorHost** kullanır hello verilerden **Deviceınfo** akış analizi işine toomanage hello eşitleme.

## <a name="solution-portal"></a>Çözüm portalı

![çözüm portalı][img-dashboard]

Merhaba çözümü olan bir web tabanlı bir kullanıcı Arabirimi toohello bulut hello önceden yapılandırılmış çözümün bir parçası dağıtılan portalıdır. Şunları yapmanızı sağlar:

* Bir panoda telemetri ve uyarı geçmişini görüntüleme.
* Yeni cihazları hazırlama.
* Cihazları yönetme ve izleme.
* Komutları toospecific aygıtları gönderin.
* Belirli cihazlarda yöntemleri çağırın.
* Kuralları ve eylemleri yönetme.
* Bir veya daha fazla cihazlarda işleri toorun zamanlayın.

Önceden yapılandırılmış bu çözümde hello çözüm portalı forms hello parçası **IOT çözümü arka ucu** ve hello parçası **işleme ve iş bağlantısı** hello tipik olarak [IOT çözümü Mimari][lnk-what-is-azure-iot].

## <a name="next-steps"></a>Sonraki adımlar

IoT çözümü mimarileri hakkında daha fazla bilgi için bkz. [Microsoft Azure IoT hizmetleri: Başvuru Mimarisi][lnk-refarch].

Artık hangi önceden yapılandırılmış bir çözüm biliyorsunuz olduğu başlamanıza hello dağıtarak *Uzaktan izleme* önceden yapılandırılmış çözüm: [hello önceden yapılandırılmış çözümleri kullanmaya başlama] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
