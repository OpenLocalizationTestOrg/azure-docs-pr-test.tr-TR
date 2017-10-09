---
title: "Azure IOT Hub aaaUnderstand doğrudan yöntemleri | Microsoft Docs"
description: "Geliştirici Kılavuzu - cihazlarınızda service uygulamasından doğrudan yöntemleri tooinvoke kod kullanın."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Anlama ve IOT hub'ı doğrudan yöntemleri çağırma
## <a name="overview"></a>Genel Bakış
IOT hub'ı hello buluta cihazlarda özelliği tooinvoke doğrudan yöntemleri sağlar. Doğrudan yöntemleri HTTP çağrı başarılı veya başarısız hemen (bir kullanıcı tarafından belirtilen zaman aşımından sonra), bir cihaz benzer tooan istek-yanıt etkileşim temsil eder. Acil eylem hello seyri hello aygıt bir aygıtı (çevrimdışı SMS yöntem çağrısı daha pahalı olması) ise bir SMS Uyandırma tooa aygıt gönderme gibi mümkün toorespond olmasına bağlı olarak farklı olduğu senaryolar için kullanışlıdır.

Her cihaz yöntemi tek bir cihazı hedefler. [İşlerini] [ lnk-devguide-jobs] şekilde tooinvoke birden fazla cihazda doğrudan yöntemleri sağlar ve zamanlama yöntem çağırma bağlantısı kesilmiş aygıtları için.

Herkesle **service bağlanma** IOT Hub üzerindeki izinleri bir aygıtta bir yöntemi çağırma.

### <a name="when-toouse"></a>Zaman toouse
Doğrudan yöntemleri bir istek-yanıt desen izleyin ve kendi sonucunun hello aygıtın, örneğin tooturn fan üzerinde genellikle etkileşimli denetimini hemen onay gerektiren iletişimleri için yöneliktir.

Çok başvuran[bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] istenen özelliklerini kullanarak arasında emin değilseniz, yöntemler veya Bulut-cihaz iletilerini doğrudan.

## <a name="method-lifecycle"></a>Yöntem yaşam döngüsü
Doğrudan yöntemleri hello aygıtta uygulanır ve sıfır gerektirebilir veya hello yöntemi yükü toocorrectly içinde daha fazla giriş örneği. Bir hizmet dönük URI üzerinden doğrudan bir yöntemi çağırma (`{iot hub}/twins/{device id}/methods/`). Bir aygıt bir aygıta özgü MQTT konu aracılığıyla doğrudan yöntemleri alır (`$iothub/methods/POST/{method name}/`). Doğrudan yöntemleri protokollerine ek cihaz tarafındaki ağ hello gelecekteki destekliyoruz.

> [!NOTE]
> Bir cihazda doğrudan bir yöntemini çağırdığınızda, özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir kümesi aşağıdaki hello birinde dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Doğrudan yöntemleri zaman uyumlu ve ya da başarılı veya başarısız hello zaman aşımı süresinden sonra (varsayılan: 30 saniye, too3600 saniyeleri ayarlanabilir). Doğrudan yöntemler, bir Phone ışığı kapatma gibi çevrimiçi ve alıcı komutları hello aygıttır ve yalnızca, bir aygıt tooact istediğiniz etkileşimli senaryolarda kullanışlıdır. Merhaba bulut hizmeti hello sonucuna mümkün olan en kısa sürede hareket etmesini sağlamak bu senaryolarda, toosee bir hemen başarı veya başarısızlık istiyor. Merhaba aygıt hello yöntemi sonucunda bazı ileti gövdesi döndürebilir ancak hello yöntemi toodo için gerekli değildir şekilde. Garanti sıralama üzerinde veya tüm eşzamanlılık semantiği yöntem çağrılarını üzerinde yok.

Doğrudan yöntemini yalnızca HTTP hello bulut taraftaki ve yalnızca MQTT hello aygıt taraftaki.

yöntem istekleri ve yanıtları için Hello yükü too8KB yukarı JSON belgedir.

## <a name="reference-topics"></a>Başvuru konuları:
Merhaba aşağıdaki başvuru konuları doğrudan yöntemler kullanma hakkında daha fazla bilgi sağlar.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Bir arka uç uygulamasından doğrudan bir yöntem çağırma
### <a name="method-invocation"></a>Yöntem çağırma
Bir cihazda doğrudan yöntem çağrılarını oluşturan HTTP çağrıları vardır:

* Merhaba *URI* belirli toohello aygıt (`{iot hub}/twins/{device id}/methods/`)
* Merhaba POST *yöntemi*
* *Üstbilgileri* hello yetkilendirme içeren, istek kimliği, içerik türü ve içerik kodlaması
* Saydam JSON *gövde* biçimini izleyen hello içinde:

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

Zaman aşımı saniye cinsindendir. Zaman aşımı ayarlanmamışsa too30 varsayılan olarak saniye.

### <a name="response"></a>Yanıt
Merhaba arka uç uygulama içeren bir yanıt alır:

* *HTTP durum kodu*, IOT hub'ı hello gelen hatalara kullanıldığı, 404 hatası cihazlar için şu anda da dahil olmak üzere bağlı
* *Üstbilgileri* hello ETag içeren, istek kimliği, içerik türü ve içerik kodlaması
* JSON *gövde* biçimini izleyen hello içinde:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Her ikisi de `status` ve `body` hello aygıt tarafından sağlanan ve toorespond hello cihazın kendi durum kodu ve/veya açıklama ile kullanılır.

## <a name="handle-a-direct-method-on-a-device"></a>Bir cihazda doğrudan bir yöntem işleme
### <a name="method-invocation"></a>Yöntem çağırma
Cihazlar hello MQTT konuda doğrudan yöntem isteği alır:`$iothub/methods/POST/{method name}/?$rid={request id}`

hangi hello aygıtından alan hello gövde biçimi aşağıdaki hello şöyledir:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Yöntemi, QoS 0 isteklerdir.

### <a name="response"></a>Yanıt
Merhaba cihaz gönderir yanıtları çok`$iothub/methods/res/{status}/?$rid={request id}`, burada:

* Merhaba `status` hello aygıt tarafından sağlanan durumunu yöntemi yürütme bir özelliktir.
* Merhaba `$rid` hello isteği IOT Hub'ından alınan hello yöntemi çağırma Kimliğinden bir özelliktir.

Merhaba gövde hello aygıt tarafından ayarlanır ve herhangi bir durum olabilir.

## <a name="additional-reference-material"></a>Ek başvuru bilgileri
Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:

* [IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.
* [Azaltma ve kotaları] [ lnk-quotas] toohello IOT Hub hizmetine uygulamak ve hello hizmetini kullandığınızda azaltma davranışı tooexpect hello hello kotaları açıklar.
* [Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.
* [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] hello tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz IOT hub'ı sorgu dili açıklar.
* [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Şimdi nasıl toouse doğrudan yöntemleri, IOT Hub Geliştirici Kılavuzu konusundaki aşağıdaki hello ilgilenebilirsiniz öğrendiniz:

* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticiyi izleyerek hello ilgilenen olabilir:

* [Doğrudan yöntemleri kullanın][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
