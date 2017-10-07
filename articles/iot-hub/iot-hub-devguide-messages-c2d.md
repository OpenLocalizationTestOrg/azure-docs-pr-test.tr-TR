---
title: "Azure IOT Hub bulut-cihaz aaaUnderstand Mesajlaşma | Microsoft Docs"
description: "Geliştirici Kılavuzu - nasıl toouse bulut IOT Hub ile Mesajlaşma cihaza. Merhaba ileti yaşam döngüsü ve yapılandırma seçenekleri hakkında bilgi içerir."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>IOT Hub'ından bulut cihaza ileti gönderme

toosend tek yönlü bildirimleri toohello aygıt, çözüm arka ucu uygulamadan IOT hub tooyour aygıtınızdan bulut aygıtları ileti gönderme. IOT Hub tarafından desteklenen diğer bulut aygıtları seçenekleri tartışma için bkz [bulut-cihaz iletişimi Kılavuzu][lnk-c2d-guidance].

Bir hizmet'e yönelik uç noktası aracılığıyla bulut cihaz göndermek (**/iletileri/devicebound**). Bir aygıt sonra hello iletileri bir cihaza özel uç noktası aracılığıyla alır (**/devices/ {DeviceID} / iletileri/devicebound**).

Her bulut cihaz ileti tek bir aygıt ayarı hello tarafından hedeflenen **için** özelliği çok**/devices/ {DeviceID} / iletileri/devicebound**.

Her cihaz sıra en çok 50 bulut-cihaz iletilerini tutar. Aynı aygıt, daha fazla ileti toohello toosend çalışılırken bir hatayla sonuçlanır.

## <a name="hello-cloud-to-device-message-lifecycle"></a>Merhaba bulut cihaz ileti yaşam döngüsü

tooguarantee en az bir kere ileti teslimi, IOT Hub cihaz başına sıralardaki bulut-cihaz iletilerini devam ettirir. Aygıtları gerekir açıkça onaylarsınız *tamamlama* IOT hub'ı tooremove için bunlardan sıra hello. Bu yaklaşım bağlantısı ve aygıt hatalarına karşı dayanıklılık güvence altına alır.

Merhaba Aşağıdaki diyagramda hello yaşam döngüsü durumu grafiği bulut cihaz iletinin IOT Hub ' gösterir.

![Bulut cihaz ileti yaşam döngüsü][img-lifecycle]

Bir ileti tooa aygıt, hello hizmet hello IOT Hub hizmeti gönderdiğinde hello ileti durumu çok ayarlar**sıraya alınan**. Bir aygıt istediği çok zaman*almak* IOT hub'ı bir ileti *kilitleri* selamlama iletisine (Merhaba durumu çok ayarlayarak**görünmez**), hello aygıt toostart üzerinde başka bir iş parçacığı sağlar diğer ileti alma. Bir aygıt iş parçacığı bir ileti hello işlenmesi tamamlandığında, IOT Hub tarafından bildirir *Tamamlanıyor* hello ileti. IOT hub'ı sonra ayarlar hello durumu çok**tamamlandı**.

Bir aygıt de seçebilirsiniz:

* *Reddetme* IOT hub'ı tooset neden selamlama iletisine onu toohello **Deadlettered** durumu. Merhaba MQTT Protokolü bağlanan aygıtları bulut-cihaz iletilerini reddedemezsiniz.
* *Abandon* IOT hub'ı tooput selamlama iletisine geri hello kuyrukta çok ayarlamak hello durumuyla neden olan selamlama iletisine**sıraya alınan**.

Bir iş parçacığı, IOT hub'ı bildirmeden tooprocess bir ileti başarısız olabilir. Bu durumda, iletileri otomatik olarak hello geçiş **görünmez** durumu geri toohello **sıraya alınan** sonra durum bir *görünürlük (veya kilidi) zaman aşımı*. Bu zaman aşımı Hello varsayılan değeri bir dakikadır.

Bir ileti hello arasında geçiş yapabilir **sıraya alınan** ve **görünmez** durumlar için en fazla kaç kez hello belirtilen hello **maksimum teslimat sayısı** IOT hub'ındaki özelliği. Çok selamlama iletisine hello durumunu geçişleri sayıdaki sonra IOT hub'ı ayarlar**Deadlettered**. Benzer şekilde, IOT hub'ı bir ileti hello durumunu çok ayarlar**Deadlettered** kendi sona erme zamanı sonra (bkz [zaman toolive][lnk-ttl]).

Merhaba [toosend bulut-cihaz IOT Hub ile nasıl iletileri] [ lnk-c2d-tutorial] nasıl hello toosend bulut cihaza iletilerden Bulut ve bunları bir aygıtta almak gösterir.

Genellikle, selamlama iletisine Hello kaybı hello uygulama mantığını etkilemez sırada bir aygıt bir bulut cihaz ileti tamamlar. Örneğin, ne zaman hello aygıt hello ileti içeriği yerel olarak kalıcı veya bir işlem başarıyla yürütüldü. Selamlama iletisine geçici bilgi, kaybı, Merhaba uygulaması hello işlevselliğini etkileyen değil, ayrıca taşımak. Bazı durumlarda, uzun süre çalışan görevler için hello bulut aygıt iletisi kalıcı sonra tamamlayabileceğiniz hello yerel depolama alanındaki görev açıklaması. Ardından hello görev ilerlemesini çeşitli aşamalarında hello çözüm arka ucu bir veya daha fazla cihaz bulut iletilerini bildirebilir.

## <a name="message-expiration-time-toolive"></a>İleti geçerlilik süresi (saat toolive)

Her bulut cihaz iletinin sona erme süresi vardır. Bu süre hello hizmeti tarafından ayarlanır (Merhaba içinde **ExpiryTimeUtc** özelliği), veya IOT Hub'ın hello varsayılan kullanarak *zaman toolive* bir IOT Hub özelliği olarak belirtilen. Bkz: [bulut cihaz yapılandırma seçenekleri][lnk-c2d-configuration].

Yaygın bir şekilde tootake avantajlarından iletisi süre sonu ve toodisconnected aygıtları ileti gönderilmesini önlemek, kısa süre toolive değerleri tooset değildir. Bu yaklaşım hello daha verimli devam ederken hello aygıt bağlantı durumunu koruma olarak aynı sonucu elde eder. İleti onayları istediğinde, IOT hub'ı mümkün tooreceive iletileri aygıtlardır ve hangi cihazların çevrimiçi olmayan ya da başarısız olmuş bildirir.

## <a name="message-feedback"></a>İleti geri bildirim

Bir bulut cihaz ileti gönderirken hello hizmet hello son durum söz konusu iletinin ilgili her ileti geri bildirim hello teslimini isteyebilirler.

| ACK özelliği | Davranışı |
| ------------ | -------- |
| **pozitif** | IOT Hub varsa ve hello bulut aygıt iletisi hello ulaştıysanız, yalnızca, bir geri bildirim iletisi oluşturur **tamamlandı** durumu. |
| **negatif** | IOT hub'ı hello bulut aygıt iletisi hello varsa ve yalnızca ulaşırsa, bir geri bildirim iletisi oluşturur **Deadlettered** durumu. |
| **tam**     | IOT Hub, her iki durumda da bir geri bildirim iletisi oluşturur. |

Varsa **Ack** olan **tam**ve geri bildirim iletisini alırsınız yok, bu hello geri bildirim iletisi süresi anlamına gelir. Merhaba hizmet ne oldu toohello özgün ileti bilemezsiniz. Uygulamada, bir hizmet süresi dolmadan önce onu hello geri bildirim işleyebilir emin olmalısınız. Merhaba maksimum süre sonu zamanı iki, Eskinin bir hata oluşursa tooget hello hizmeti yeniden çalışmasını sağlayan gündür.

İçinde anlatıldığı gibi [uç noktaları][lnk-endpoints], IOT hub'ı sunan bir hizmet'e yönelik uç noktası aracılığıyla geribildirim (**/messages/servicebound/feedback**) iletileri olarak. Merhaba geri bildirim alma semantiğini olan hello aynı bulut-cihaz iletilerini ettirilmesi ve sahip, hello aynı [ileti yaşam döngüsü][lnk-lifecycle]. Mümkün olduğunda, tek bir iletiye ileti geri bildirim biçimi aşağıdaki hello ile toplu:

| Özellik     | Açıklama |
| ------------ | ----------- |
| EnqueuedTime | Selamlama iletisine ne zaman oluşturulduğunu belirten bir zaman damgası. |
| Kullanıcı Kimliği       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

Merhaba gövdesi bir JSON serileştirilmiş dizisi kayıtları, her hello aşağıdaki özelliklere sahip olan:

| Özellik           | Açıklama |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | Ne zaman selamlama iletisine hello sonucunu oldu belirten bir zaman damgası. Örneğin, aygıt tamamlandı hello veya selamlama iletisine süresi. |
| OriginalMessageId  | **MessageID** hello bulut aygıt iletisi toowhich bu geri bildirim bilgilerini ilişkilendirir. |
| statusCode         | Gerekli dize. IOT Hub tarafından oluşturulan geri bildirim iletileri kullanılır. <br/> 'Başarılı' <br/> 'Süresi' <br/> 'DeliveryCountExceeded' <br/> 'Reddedildi' <br/> 'Temizlendi' |
| Açıklama        | Dize değerlerini **StatusCode**. |
| Cihaz kimliği           | **DeviceID** bu aldığımız geri Bildirimlerden biri hello bulut aygıt iletisi toowhich, hedef aygıtın hello ilişkilendirir. |
| DeviceGenerationId | **DeviceGenerationId** bu aldığımız geri Bildirimlerden biri hello bulut aygıt iletisi toowhich, hedef aygıtın hello ilişkilendirir. |

Merhaba hizmet belirtmelisiniz bir **MessageID** kendi geri bildirim hello özgün iletiyle toobe mümkün toocorrelate hello bulut cihaz iletisi için.

Merhaba aşağıdaki örnek bir geri bildirim iletisinin gövdesinde hello gösterir.

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>Bulut cihaz yapılandırma seçenekleri

Her IOT hub'ı bulut cihaz Mesajlaşma için yapılandırma seçenekleri aşağıdaki hello sunar:

| Özellik                  | Açıklama | Aralık ve varsayılan |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | Bulut-cihaz iletilerini için varsayılan TTL değeri. | Too2D ISO_8601 aralığı (en az 1 dakika). Varsayılan: 1 saat. |
| maxDeliveryCount          | Maksimum teslimat sayısı her aygıt için bulut cihaz sıralar. | 1 too100. Varsayılan: 10. |
| feedback.ttlAsIso8601     | Hizmet bağlı geri bildirim iletileri için bekletme. | Too2D ISO_8601 aralığı (en az 1 dakika). Varsayılan: 1 saat. |
| feedback.maxDeliveryCount |Geri bildirim kuyruğu en yüksek teslimat sayısı. | 1 too100. Varsayılan: 100. |

Bu yapılandırma seçenekleri tooset nasıl görürüm hakkında daha fazla bilgi için [oluşturma IOT hub'ları][lnk-portal].

## <a name="next-steps"></a>Sonraki adımlar

Merhaba SDK'ları hakkında bilgi için tooreceive bulut-cihaz iletilerini kullanın, bkz: [Azure IOT SDK'ları][lnk-sdks].

Bulut-cihaz iletilerini alma çıkışı tootry bkz hello [Gönder bulut cihaz] [ lnk-c2d-tutorial] Öğreticisi.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
