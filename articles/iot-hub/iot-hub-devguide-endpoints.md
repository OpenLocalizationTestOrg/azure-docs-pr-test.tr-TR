---
title: "aaaUnderstand Azure IOT Hub uç noktaları | Microsoft Docs"
description: "Geliştirici Kılavuzu - IOT Hub hakkında başvuru bilgileri aygıt bakan ve hizmeti kullanıma yönelik uç noktalar."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>Başvuru - IOT Hub uç noktaları

## <a name="iot-hub-names"></a>IOT Hub adları

Hello hello portalında uç noktalarınızı barındıran hello IOT hub'hello adı bulabilirsiniz **genel bakış** dikey. Varsayılan olarak, IOT hub'ı hello DNS adı aşağıdaki gibi görünür: `{your iot hub name}.azure-devices.net`.

Azure DNS toocreate IOT hub'ınız için özel bir DNS adı kullanabilirsiniz. Daha fazla bilgi için bkz: [bir Azure hizmeti Azure DNS'yi tooprovide özel etki alanı ayarlarını](../dns/dns-custom-domain.md#azure-iot).

## <a name="list-of-built-in-iot-hub-endpoints"></a>Yerleşik IOT Hub uç noktaları listesi

Azure IOT Hub kendi işlevselliği toovarious aktörler gösteren çok kiracılı bir hizmettir. Merhaba Aşağıdaki diyagramda hello IOT hub'ı sunan çeşitli uç noktaları gösterilmektedir.

![IoT Hub uç noktaları][img-endpoints]

liste aşağıdaki hello hello uç noktalar açıklanmaktadır:

* **Kaynak sağlayıcısı**. Merhaba IOT hub'ı kaynak sağlayıcısı sunan bir [Azure Resource Manager] [ lnk-arm] arabirimi. Bu arabirim, Azure abonelik sahipleri toocreate sağlar ve IOT hub'ları ve tooupdate IOT hub'ı özelliklerini silin. IOT hub'ı özelliklerini yöneten [hub düzeyindeki güvenlik ilkeleri][lnk-accesscontrol], toodevice düzeyi erişim denetimi ve bulut-cihaz ve cihaz bulut Mesajlaşma işlevsel seçeneklerini aygıtlardır. Merhaba IOT hub'ı kaynak sağlayıcısı ayrıca çok sağlar[cihaz kimliklerini verme][lnk-importexport].
* **Cihaz Kimlik Yönetimi**. Her IOT hub'ı HTTP REST uç noktaları toomanage cihaz kimlikleri kümesi sunar (oluşturma, alma, güncelleştirme ve silme). [Cihaz kimliklerini] [ lnk-device-identities] cihaz kimlik doğrulaması ve erişim denetimi için kullanılır.
* **Cihaz çifti Yönetimi**. Her IOT hub'ı kullanıma sunan bir dizi hizmet dönük HTTP REST uç noktası tooquery ve güncelleştirme [cihaz çiftlerini] [ lnk-twins] (güncelleştirme etiketleri ve özellikleri).
* **İşlerini Yönetim**. Her IOT hub hizmeti dönük HTTP REST uç noktası tooquery kümesini gösterir ve yönetme [işleri][lnk-jobs].
* **Cihaz uç noktaları**. Merhaba kimlik kayıt defterinde her cihaz için IOT Hub uç noktalar kümesi sunar:

  * *Cihaz bulut iletilerini göndermek*. Bir aygıt bu uç nokta çok kullanır[cihaz bulut iletilerini göndermek][lnk-d2c].
  * *Bulut-cihaz iletilerini*. Bir aygıtın hedeflenen Bu uç nokta tooreceive kullandığı [bulut-cihaz iletilerini][lnk-c2d].
  * *Dosya yüklemeleri başlatmak*. Bir aygıt bu uç nokta tooreceive bir Azure depolama SAS URI'sini IOT hub'dan çok kullanır[bir dosyayı karşıya yüklemeyi][lnk-upload].
  * *Alma ve güncelleştirme cihaz çifti özellikleri*. Bir aygıt bu uç nokta tooaccess kullanan kendi [cihaz çifti][lnk-twins]ait özellikler.
  * *Doğrudan yöntemi isteklerini alacak*. Bir aygıt için bu uç nokta toolisten kullanan [doğrudan yöntemi][lnk-methods]'s istekleri.

    Bu uç noktalar kullanılarak kullanıma sunulan [MQTT v3.1.1][lnk-mqtt], HTTP 1.1 ve [AMQP 1.0] [ lnk-amqp] protokoller. AMQP kullanılabilir ayrıca üzerinden [WebSockets] [ lnk-websockets] bağlantı noktası 443'tür.

    yalnızca hello kullandığınızda hello cihaz çiftlerini ve yöntemleri uç noktaları kullanılabilir [MQTT v3.1.1] [ lnk-mqtt] protokolü.

* **Hizmet uç noktaları**. Her IOT hub uç noktaları için çözüm arka ucu toocommunicate kümesi cihazlarınızı kullanıma sunar. Bunun tek istisnası Bu uç noktalar yalnızca hello kullanarak gösterilen [AMQP] [ lnk-amqp] protokolü. Merhaba yöntemi çağırma endpoint hello HTTP protokolü açıktır.
  
  * *Cihaz bulut iletilerini*. Bu uç nokta ile uyumlu [Azure Event Hubs][lnk-event-hubs]. Bir arka uç hizmeti tooread hello kullanabilirsiniz [cihaz bulut iletilerini] [ lnk-d2c] cihazlar tarafından gönderilen. Özel uç noktaları, IOT hub'ına ek toothis yerleşik uç oluşturabilirsiniz.
  * *Bulut-cihaz iletilerini göndermek ve teslim alındı bildirimleri almak*. Bu uç noktalar, çözüm arka ucu toosend güvenilir etkinleştirmek [bulut-cihaz iletilerini][lnk-c2d], ve tooreceive hello karşılık gelen teslim veya sona erme ilgili kaynaklar.
  * *Dosya bildirimlerin*. Aygıtlarınızı başarıyla bir dosyayı karşıya yüklediğinizde bu Mesajlaşma uç tooreceive bildirimleri sağlar. 
  * *Yöntem çağırma doğrudan*. Bu uç noktaya bir arka uç hizmetine tooinvoke sağlayan bir [doğrudan yöntemi] [ lnk-methods] bir aygıtta.
  * *Alma olaylarını izleme işlemleri*. Bu uç nokta izleme olayları, IOT hub süredir tooemit yapılandırdıysanız tooreceive işlemlere izin verir bunları. Daha fazla bilgi için bkz: [izleme IOT hub'ı operations][lnk-operations-mon].

Merhaba [Azure IOT SDK'ları] [ lnk-sdks] makalede bu uç noktalar çeşitli yolları tooaccess hello.

Tüm IOT Hub uç noktaları hello kullan [TLS] [ lnk-tls] protokolü ve uç nokta yok şifrelenmemiş ve güvenli kanallar üzerinde gösterilen herhangi bir zamanda.

## <a name="custom-endpoints"></a>Özel uç noktaları

İleti yönlendirme için uç noktalar olarak, abonelik tooyour IOT hub tooact mevcut Azure hizmetlerine bağlayabilirsiniz. Bu uç noktalar hizmet uç noktalar olarak hareket ve iç havuzlar ileti yollar için kullanılır. Cihazları doğrudan ek uç noktaları toohello yazamıyor. ileti yollar hakkında daha fazla toolearn bakın hello Geliştirici Kılavuzu girişi [IOT hub ile ileti gönderme ve alma][lnk-devguide-messaging].

IOT hub'ı şu anda Azure hizmetlerine ek uç noktalar olarak aşağıdaki hello destekler:

* Event Hubs
* Service Bus Kuyrukları
* Service Bus Konuları

IOT hub'ı yazma erişimi toothese hizmet uç noktaları için ileti yönlendirme toowork gerekir. Noktalarınızı hello Azure portal aracılığıyla yapılandırırsanız, hello gerekli izinleri sizin için eklenir. Hizmetleri toosupport beklenen hello verimlilik yapılandırdığınızdan emin olun. IOT çözümünüzü ilk yapılandırırken, ek noktalarınızı toomonitor gerekir ve hello gerçek yükleme için gerekli ayarlamaları yapın.

Bir ileti birden çok yol tüm toohello noktası eşleşiyorsa aynı uç noktası, IOT hub'ı sunar ileti toothat uç nokta yalnızca bir kez. Bu nedenle, değil gerek tooconfigure yinelenenleri kaldırmayı hizmet veri yolu kuyruğu ya da konu yapın. Bölümlenmiş sıralarındaki bölüm benzeşim ileti sıralama güvence altına alır.

> [!NOTE]
> Service Bus kuyrukları ve konularından IOT Hub uç noktaları değil olarak kullanılan **oturumları** veya **yinelenen saptama** etkin. Bu seçeneklerden birini etkinleştirilirse hello uç noktası olarak görünür **ulaşılamıyor** hello Azure Portalı'nda.

Uç noktalar ekleyebilirsiniz hello sayısına Hello sınırları için bkz: [kotalar ve azaltma][lnk-devguide-quotas].

## <a name="field-gateways"></a>Alan ağ geçitleri

Bir IOT çözümündeki bir *alan ağ geçidi* , cihazlarınız ve IOT Hub uç noktaları arasında bulunur. Genellikle bulunduğu Kapat tooyour cihazlarda desteklenir. Aygıtlarınızı hello cihazlar tarafından desteklenen bir protokolü kullanarak doğrudan hello alan ağ geçidi ile iletişim kurar. Merhaba alan ağ geçidi tooan IOT hub'ı uç IOT Hub tarafından desteklenen bir protokol kullanılarak bağlanır. Bir alan ağ geçidi, adanmış bir donanımsal cihaz veya özel ağ geçidi yazılımını çalıştıran bir düşük güç bilgisayar olabilir.

Kullanabileceğiniz [Azure IOT kenar] [ lnk-iot-edge] tooimplement bir alan ağ geçidi. IOT kenar hello üzerine birden çok aygıt iletişimlerinden çoğullama gibi işlevselliği sunar aynı IOT Hub bağlantısı.

## <a name="next-steps"></a>Sonraki adımlar

Bu IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:

* [Cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili][lnk-devguide-query]
* [Kotalar ve azaltma][lnk-devguide-quotas]
* [IOT Hub MQTT desteği][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
