---
title: "aaaUse ölçümleri toomonitor Azure IOT Hub | Microsoft Docs"
description: "IOT hub'larınız genel durumunu nasıl toouse Azure IOT Hub ölçümleri tooassess ve İzleyicisi Merhaba."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>IOT hub'ı ölçümleri anlama
IOT hub'ı ölçümleri Azure aboneliğinizde hello Azure IOT kaynakları hello durumuyla ilgili daha iyi veri verin. IOT hub'ı ölçümleri etkinleştir, tooassess hello IOT Hub hizmeti ve hello cihazların genel durumunu hello tooit bağlı. IOT hub ve Yardım kök neden sorunlarınızı toocontact Azure desteğine gerek kalmadan neler olup bittiğini görmenize yardımcı olmak için kullanıcı dönük istatistikleri önemlidir.

Ölçümleri varsayılan olarak etkinleştirilir. IOT Hub'hello Azure portal ölçümleri görüntüleyebilirsiniz.

## <a name="how-tooview-iot-hub-metrics"></a>Nasıl tooview IOT hub'ı ölçümleri
1. IOT hub'ı oluşturun. Hakkında yönergeler bulabilirsiniz toocreate bir IOT hub'hello [Get Started] [ lnk-get-started] Kılavuzu.
2. IOT hub'ınızı Hello dikey penceresini açın. Buradan, tıklatın **ölçümleri**.
   
    ![][1]
3. Merhaba ölçümleri dikey penceresinden için IOT hub'ınızı hello ölçümleri görüntüleyin ve ölçümlerinizi özel görünümler oluşturun. Toosend ölçümleri veri tooan olay hub'ları uç noktası veya bir Azure depolama hesabı tıklayarak seçebileceğiniz **tanılama ayarları**.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>IOT hub'ı ölçümleri ve nasıl toouse bunları
IOT hub'ı çeşitli ölçümleri sağlar, hello durumunu hub ve hello genel bir bakış toplam sayısı toogive bağlı cihazları. Birden çok ölçümleri toopaint hello IOT hub'ının hello durumunun daha kapsamlı bir resim bilgilerinden birleştirebilirsiniz. Aşağıdaki tablonun hello her IOT hub'ı izler hello ölçümleri açıklar ve her ölçümü toohello genel ilişkili nasıl durumunu hello IOT hub'ı.

|Ölçüm|Ölçüm görünen adı|Birim|Toplama türü|Açıklama|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Telemetri ileti gönderme denemeleri|Sayı|Toplam|Gönderilen tooyour IOT hub cihaz bulut telemetri iletilerini denenen toobe sayısı|
|d2c.telemetry.ingress.Success|Gönderilen telemetri iletilerini|Sayı|Toplam|Başarıyla gönderilen tooyour IOT hub cihaz bulut telemetri iletilerini sayısı|
|c2d.Commands.egress.Complete.Success|Tamamlanan komutları|Sayı|Toplam|Merhaba aygıt tarafından başarıyla tamamlandı bulut cihaz komutlarının sayısı|
|c2d.Commands.egress.Abandon.Success|Terk komutları|Sayı|Toplam|Merhaba aygıt tarafından terk bulut cihaz komutlarının sayısı|
|c2d.Commands.egress.Reject.Success|Reddedilen komutları|Sayı|Toplam|Merhaba aygıt tarafından reddedilen bulut cihaz komutlarının sayısı|
|devices.totalDevices|Toplam aygıt|Sayı|Toplam|Tooyour IOT hub'ı kayıtlı aygıtların sayısı|
|devices.connectedDevices.allProtocol|Bağlı aygıtlar|Sayı|Toplam|Tooyour IOT hub'ı bağlı aygıt sayısı|
|d2c.telemetry.egress.Success|Telemetri iletilerini teslim|Sayı|Toplam|İletileri başarıyla tooendpoints (toplam) yazılmış sayısı|
|d2c.telemetry.egress.dropped|Bırakılan iletiler|Sayı|Toplam|Tüm yollar eşleşmedi ve hello geri dönüş rota devre dışı bırakıldı kesilen iletisi sayısı|
|d2c.telemetry.egress.orphaned|Yalnız bırakılmış ileti|Sayı|Toplam|Merhaba hello geri dönüş yolu da dahil olmak üzere tüm yollar eşleşmeyen ileti sayısı|
|d2c.telemetry.egress.invalid|Geçersiz iletileri|Sayı|Toplam|Merhaba ileti sayısı nedeniyle teslim edilmedi tooincompatibility hello uç noktası ile|
|d2c.telemetry.egress.fallback|Geri dönüş koşulla eşleşen iletileri|Sayı|Toplam|Toohello geri dönüş endpoint yazılan ileti sayısı|
|d2c.endpoints.egress.eventHubs|Hub uç noktaları tooEvent iletiler teslim|Sayı|Toplam|İletileri başarıyla yazılı tooEvent Hub uç noktaları olan sayısı|
|d2c.endpoints.latency.eventHubs|Olay hub'ı uç noktaları için ileti gecikme süresi|milisaniye|Ortalama|Merhaba ortalama gecikme süresi ileti giriş toohello IOT hub ve ileti giriş arasındaki milisaniye cinsinden bir olay hub'ı uç içine|
|d2c.endpoints.egress.serviceBusQueues|İleti veri yolu kuyruğu uç noktaları tooService teslim|Sayı|Toplam|İletileri başarıyla yazılı tooService veri yolu kuyruğu uç noktaları olan sayısı|
|d2c.endpoints.latency.serviceBusQueues|Hizmet veri yolu kuyruğu uç noktalar için ileti gecikme süresi|milisaniye|Ortalama|Merhaba ortalama gecikme süresi ileti giriş toohello IOT hub ve ileti giriş arasındaki milisaniye olarak bir hizmet veri yolu kuyruğu uç noktası içine|
|d2c.endpoints.egress.serviceBusTopics|İleti veri yolu konusu uç noktaları tooService teslim|Sayı|Toplam|İletileri başarıyla yazılı tooService veri yolu konusu uç noktaları olan sayısı|
|d2c.endpoints.latency.serviceBusTopics|Hizmet veri yolu konusu uç noktalar için ileti gecikme süresi|milisaniye|Ortalama|Merhaba ortalama gecikme süresi ileti giriş toohello IOT hub ve ileti giriş arasındaki milisaniye olarak bir hizmet veri yolu konusu uç noktası içine|
|d2c.endpoints.egress.builtIn.events|Toohello yerleşik uç noktası (iletileri/olayları) teslim edilen ileti|Sayı|Toplam|İletileri başarıyla yazılı toohello yerleşik uç noktası (iletileri/olayları) olan sayısı|
|d2c.endpoints.latency.builtIn.events|İleti gecikme hello yerleşik uç noktası (iletileri/olayları) için|milisaniye|Ortalama|Merhaba ortalama gecikme süresi arasında ileti giriş toohello IOT hub ve ileti giriş hello yerleşik uç noktası (iletileri/olayları), milisaniye cinsinden içine |
|d2c.Twin.Read.Success|Başarılı twin aygıtlardan okur|Sayı|Toplam|tüm başarılı aygıt tarafından başlatılan twin Hello sayısını okur.|
|d2c.Twin.Read.failure|Aygıtlardan Twin okuma başarısız oldu|Sayı|Toplam|Merhaba sayımını tüm aygıt tarafından başlatılan twin okuma başarısız oldu.|
|d2c.Twin.Read.size|Aygıtlardan twin yanıt boyutu okur|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı değeri aygıt tarafından başlatılan okuma çifti.|
|d2c.Twin.Update.Success|Aygıtlardan başarılı twin güncelleştirmeleri|Sayı|Toplam|Merhaba tüm başarılı twin aygıt tarafından başlatılan güncelleştirme sayısı.|
|d2c.Twin.Update.failure|Aygıtlardan Twin güncelleştirmeler başarısız oldu|Sayı|Toplam|Merhaba sayımını tüm aygıt tarafından başlatılan twin güncelleştirmeler başarısız oldu.|
|d2c.Twin.Update.size|Aygıtlardan twin güncelleştirmeleri boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max boyutu tüm başarılı aygıt tarafından başlatılan güncelleştirmeleri çifti.|
|c2d.methods.Success|Başarılı doğrudan yöntem çağrıları|Sayı|Toplam|tüm başarılı doğrudan yöntem çağrılarını Hello sayısı.|
|c2d.methods.failure|Doğrudan yöntem çağrılarını başarısız oldu|Sayı|Toplam|Tüm Hello sayısı doğrudan yöntem çağrıları başarısız oldu.|
|c2d.methods.requestSize|Doğrudan yöntem çağrılarını isteği boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı doğrudan yöntemi istekleri.|
|c2d.methods.responseSize|Doğrudan yöntem çağrılarını yanıt boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı doğrudan yöntem yanıtların.|
|c2d.Twin.Read.Success|Arka ucunuzdan başarılı twin okur|Sayı|Toplam|tüm başarılı arka uç başlatılan twin Hello sayısını okur.|
|c2d.Twin.Read.failure|Arka ucunuzdan başarısız twin okur|Sayı|Toplam|Merhaba sayımını tüm arka uç başlatılan twin okuma başarısız oldu.|
|c2d.Twin.Read.size|Arka uç twin okuma yanıt boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max tüm başarılı, arka uç başlatılan okuma çifti.|
|c2d.Twin.Update.Success|Arka uç başarılı twin güncelleştirmeleri|Sayı|Toplam|Merhaba tüm başarılı twin arka uç başlatılan güncelleştirme sayısı.|
|c2d.Twin.Update.failure|Arka uç başarısız twin güncelleştirmeleri|Sayı|Toplam|Merhaba sayımını tüm arka uç başlatılan twin güncelleştirmeler başarısız oldu.|
|c2d.Twin.Update.size|Arka uç twin güncelleştirmelerini boyutu|Bayt|Ortalama|Merhaba ortalama, min ve max boyutu tüm başarılı arka uç başlatılan güncelleştirmeleri çifti.|
|twinQueries.success|Başarılı twin sorguları|Sayı|Toplam|tüm başarılı twin sorguları Hello sayısı.|
|twinQueries.failure|Başarısız twin sorguları|Sayı|Toplam|Tüm başarısız twin sorguları Hello sayısı.|
|twinQueries.resultSize|Twin sorguları sonuç boyutu|Bayt|Ortalama|Hello ortalama, min ve max hello sonuç boyutunun tüm başarılı twin sorgular.|
|jobs.createTwinUpdateJob.success|Twin güncelleştirme işlerinin başarılı oluşturma|Sayı|Toplam|tüm başarılı twin güncelleştirme işlerinin oluşturulması Hello sayısı.|
|jobs.createTwinUpdateJob.failure|Twin güncelleştirme işlerinin başarısız oluşturma|Sayı|Toplam|tüm oluşturma işlemi başarısız twin güncelleştirme işleri Hello sayısı.|
|jobs.createDirectMethodJob.success|Yöntem çağırma işlerinin başarılı oluşturma|Sayı|Toplam|tüm başarılı doğrudan yöntemi çağırma işlerinin oluşturulması Hello sayısı.|
|jobs.createDirectMethodJob.failure|Yöntem çağırma işlerinin başarısız oluşturma|Sayı|Toplam|tüm oluşturma işlemi başarısız doğrudan yöntem çağrısını işler Hello sayısı.|
|jobs.listJobs.success|Başarılı çağrı toolist işleri|Sayı|Toplam|tüm başarılı çağrı toolist işleri Hello sayısı.|
|jobs.listJobs.failure|Başarısız çağrılar toolist işleri|Sayı|Toplam|Tüm başarısız çağrılar toolist işleri Hello sayısı.|
|jobs.cancelJob.success|Başarılı iş iptalleri|Sayı|Toplam|Merhaba sayımını tüm başarılı bir işi toocancel çağırır.|
|jobs.cancelJob.failure|Başarısız iş iptalleri|Sayı|Toplam|Tüm başarısız çağrılar toocancel bir işi Hello sayısı.|
|jobs.queryJobs.success|İş başarılı sorguları|Sayı|Toplam|tüm başarılı çağrı tooquery işleri Hello sayısı.|
|jobs.queryJobs.failure|Başarısız işi sorgular|Sayı|Toplam|Tüm başarısız çağrılar tooquery işleri Hello sayısı.|
|Jobs.Completed|Tamamlanan İşler|Sayı|Toplam|Tüm tamamlanan işler Hello sayısı.|
|Jobs.Failed|Başarısız olan işler|Sayı|Toplam|Tüm başarısız işler Hello sayısı.|

## <a name="next-steps"></a>Sonraki adımlar
IOT hub'ı ölçümleri genel bir bakış gördüğünüze göre Azure IOT hub'ı yönetme hakkında daha fazla Bu bağlantı toolearn izleyin:

* [İzleme işlemleri][lnk-monitor]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
