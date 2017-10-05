---
title: "Azure IOT hub'ı doğrudan yöntemlerini anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - kod cihazlarınızda service uygulamasından çağırmak için doğrudan yöntemlerini kullanın."
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
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Anlama ve IOT hub'ı doğrudan yöntemleri çağırma
## <a name="overview"></a>Genel Bakış
IOT Hub, bulutta cihazlarda doğrudan yöntemlerini çağırmasına olanak sağlar. Başarılı veya başarısız hemen (bir kullanıcı tarafından belirtilen zaman aşımından sonra), bir HTTP çağrısıyla benzer bir cihaz istek-yanıt etkileşim doğrudan yöntemleri temsil eder. Acil eylem seyri aygıt bir aygıtı (çevrimdışı SMS yöntem çağrısı daha pahalı olması) ise, bir SMS Uyandırma bir cihaza gönderme gibi yanıt verebilmesini olmasına bağlı olarak farklı olduğu senaryolar için kullanışlıdır.

Her cihaz yöntemi tek bir cihazı hedefler. [İşlerini] [ lnk-devguide-jobs] doğrudan yöntemlerini birden çok aygıta çağırmak için bir yol sağlar ve zamanlama yöntem çağırma bağlantısı kesilmiş aygıtları için.

Herkesle **service bağlanma** IOT Hub üzerindeki izinleri bir aygıtta bir yöntemi çağırma.

### <a name="when-to-use"></a>Kullanılması gereken durumlar
Doğrudan yöntemleri istek-yanıt desenler izleyen ve örneğin fan üzerinde etkinleştirmek aygıtın genellikle etkileşimli denetimini kendi sonucunun hemen onay gerektiren iletişimleri için yöneliktir.

Başvurmak [bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] istenen özelliklerini kullanarak arasında emin değilseniz, yöntemler veya Bulut-cihaz iletilerini doğrudan.

## <a name="method-lifecycle"></a>Yöntem yaşam döngüsü
Doğrudan yöntemleri cihazda uygulanır ve doğru örneği oluşturmak için yöntem yükte sıfır veya daha fazla girdi gerektirebilir. Bir hizmet dönük URI üzerinden doğrudan bir yöntemi çağırma (`{iot hub}/twins/{device id}/methods/`). Bir aygıt bir aygıta özgü MQTT konu aracılığıyla doğrudan yöntemleri alır (`$iothub/methods/POST/{method name}/`). Doğrudan yöntemleri ek cihaz tarafındaki ağ protokollerini temel gelecekte destekliyoruz.

> [!NOTE]
> Bir cihazda doğrudan bir yöntemini çağırdığınızda, özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir herhangi aşağıdaki kümesindeki dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Zaman uyumlu yöntemleri ve ya da başarılı doğrudan veya zaman aşımı süresinden sonra başarısız (varsayılan: 30 saniye, 3600 saniye olarak ayarlanabilir kurma). Doğrudan yöntemler, bir Phone ışığı kapatma gibi çevrimiçi ve alıcı komutları, cihaz, yalnızca ve yalnızca, görev yapması için bir aygıt istediğiniz etkileşimli senaryolarda kullanışlıdır. Bu senaryolarda, bulut hizmeti sonucuna mümkün olan en kısa sürede hareket etmesini sağlamak bir hemen başarı veya başarısızlık görmek istediğinizi açıklayın. Cihaz bazı ileti gövdesi yöntemi sonucunda döndürebilir ancak yöntemi bunu yapmak gerekli değildir. Garanti sıralama üzerinde veya tüm eşzamanlılık semantiği yöntem çağrılarını üzerinde yok.

Doğrudan yöntemini yalnızca HTTP bulut taraftaki ve yalnızca MQTT aygıt taraftaki.

Yöntem istekleri ve yanıtları için yükü, bir JSON belgesi en fazla 8 KB ' dir.

## <a name="reference-topics"></a>Başvuru konuları:
Aşağıdaki başvuru konuları doğrudan yöntemler kullanma hakkında daha fazla bilgi sağlar.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Bir arka uç uygulamasından doğrudan bir yöntem çağırma
### <a name="method-invocation"></a>Yöntem çağırma
Bir cihazda doğrudan yöntem çağrılarını oluşturan HTTP çağrıları vardır:

* *URI* aygıta belirli (`{iot hub}/twins/{device id}/methods/`)
* POST *yöntemi*
* *Üstbilgileri* yetkilendirme içeren, istek kimliği, içerik türü ve içerik kodlaması
* Saydam JSON *gövde* şu biçimde:

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

Zaman aşımı saniye cinsindendir. Zaman aşımı ayarlanmamışsa 30 saniye olarak varsayılan olarak ayarlanır.

### <a name="response"></a>Yanıt
Arka uç uygulama içeren bir yanıt alır:

* *HTTP durum kodu*, IOT Hub'ından gelen hatalara kullanıldığı, 404 hatası cihazlar için şu anda da dahil olmak üzere bağlı
* *Üstbilgileri* ETag içeren, istek kimliği, içerik türü ve içerik kodlaması
* JSON *gövde* şu biçimde:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Her ikisi de `status` ve `body` cihaz tarafından sağlanan ve cihazın kendi durum kodu ve/veya açıklama ile yanıtlamak için kullanılır.

## <a name="handle-a-direct-method-on-a-device"></a>Bir cihazda doğrudan bir yöntem işleme
### <a name="method-invocation"></a>Yöntem çağırma
Cihazlar, MQTT konusunda doğrudan yöntem isteği alır:`$iothub/methods/POST/{method name}/?$rid={request id}`

Cihaz alan gövdesi aşağıdaki biçimdedir:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Yöntemi, QoS 0 isteklerdir.

### <a name="response"></a>Yanıt
Cihaz yanıtlarını gönderir `$iothub/methods/res/{status}/?$rid={request id}`, burada:

* `status` Yöntemi yürütme aygıt tarafından sağlanan durumunu bir özelliktir.
* `$rid` IOT Hub'ından alınan yöntemi çağırma isteği Kimliğinden bir özelliktir.

Gövde aygıt tarafından ayarlanır ve herhangi bir durum olabilir.

## <a name="additional-reference-material"></a>Ek başvuru bilgileri
IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:

* [IOT Hub uç noktaları] [ lnk-endpoints] her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunan çeşitli uç noktaları açıklar.
* [Azaltma ve kotaları] [ lnk-quotas] IOT Hub hizmeti ve azaltma davranışı hizmetini kullandığınızda beklediğiniz uygulama kotaları açıklar.
* [Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] çeşitli dil IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanabilir SDK'ları listeler.
* [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] IOT Hub'ından, cihaz çiftlerini ve işleri hakkında bilgi almak için kullanabileceğiniz IOT hub'ı sorgu dili açıklar.
* [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] IOT hub'ı desteği hakkında daha fazla bilgi için MQTT Protokolü sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Doğrudan yöntemlerini kullanmayı öğrendiniz artık aşağıdaki IOT Hub Geliştirici Kılavuzu konusundaki ilgi olabilir:

* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

Bu makalede açıklanan kavramları bazıları denemek istiyorsanız, aşağıdaki IOT hub'ı öğreticide ilgilenen olabilir:

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
