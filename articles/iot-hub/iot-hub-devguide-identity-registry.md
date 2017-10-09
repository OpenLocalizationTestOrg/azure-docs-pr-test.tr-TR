---
title: "aaaUnderstand hello Azure IOT Hub kimlik kayıt defteri | Microsoft Docs"
description: "Geliştirici Kılavuzu - hello IOT Hub kimlik kayıt defteri açıklaması ve nasıl toouse, toomanage aygıtlarınızı. Toplu olarak hello içeri ve dışarı aktarma cihaz kimlikleri hakkında bilgi içerir."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>Merhaba kimlik IOT hub'ınızı kayıt defterinde anlama

Her IOT hub'ı toohello IOT hub'ı tooconnect izin hello cihazlarla ilgili bilgileri depolayan bir kimlik kayıt defteri sahiptir. Bir cihaz IOT hub'ı tooan bağlanmadan önce hello IOT hub'ın kimlik kayıt defterinde bu cihaz için bir girdi olmalıdır. Bir cihaz da hello IOT hub'ı hello kimlik kayıt defterinde depolanan kimlik bilgileri temel ile kimlik doğrulaması gerekir.

Merhaba kimlik kayıt defterinde depolanan hello cihaz kimliği büyük/küçük harf duyarlıdır.

Yüksek bir düzeyde hello kimlik kayıt defteri REST özellikli cihaz kimlik kaynakları koleksiyonudur. Bir giriş hello kimlik kayıt defterinde eklediğinizde, IOT Hub cihaz başına kaynakları yürütülen bulut-cihaz iletilerini içeren hello sırası gibi bir dizi oluşturur.

### <a name="when-toouse"></a>Zaman toouse

Gerektiğinde Merhaba kimlik kayıt defteri kullanın:

* Tooyour IOT hub bağlantı cihazları sağlamak.
* Aygıt başına erişim tooyour hub'ın aygıt'e yönelik uç noktalar denetler.

> [!NOTE]
> Merhaba kimlik kayıt defteri herhangi bir uygulamaya özgü meta veri içermiyor.

## <a name="identity-registry-operations"></a>Kimlik kayıt defteri işlemleri

Merhaba IOT Hub kimlik kayıt defteri işlemlerini aşağıdaki hello sunar:

* Cihaz kimliği oluşturma
* Güncelleştirme cihaz kimliği
* Cihaz kimliği Kimliğine göre alma
* Cihaz Kimliği Sil
* Too1000 kimlikleri listesi
* Tüm kimliklerin tooAzure blob depolama dışarı aktarma
* Azure blob depolama alanından kimlikleri alma

Bu işlemler belirtildiği gibi iyimser eşzamanlılık kullanabilirsiniz [RFC7232][lnk-rfc7232].

> [!IMPORTANT]
> yalnızca yol tooretrieve hello bir IOT hub'ın kimlik kayıt defterinde tüm kimlikleri olan toouse hello [verme] [ lnk-export] işlevselliği.

Bir IOT Hub kimlik kayıt defteri:

* Herhangi bir uygulama meta veri içermiyor.
* Bir sözlük gibi hello kullanarak erişilebilir **DeviceID** başlangıç anahtarı olarak.
* Açıklayıcı sorguları desteklemez.

Bir IOT çözüm genellikle uygulamaya özgü meta veriler içeren ayrı bir çözüme özel deposu vardır. Örneğin, hello akıllı yapı çözümü çözüme özel deposunda sıcaklık algılayıcısı dağıtıldığı hello yer kaydeder.

> [!IMPORTANT]
> Yalnızca hello kimlik kayıt defteri aygıt yönetimi ve işlemleri sağlama için kullanın. Çalışma zamanında yüksek verimlilik işlemleri hello kimlik kayıt defterinde işlemlerini gerçekleştirme üzerinde bağlı olmaması gerekir. Örneğin, bir komut göndermeden önce bir aygıt hello bağlantı durumunu denetleme desteklenen desen değil. Toocheck hello emin olun [oranları azaltma] [ lnk-quotas] hello kimlik kayıt defteri ve hello [aygıt sinyal] [ lnk-guidance-heartbeat] düzeni.

## <a name="disable-devices"></a>Cihazları devre dışı bırak

Merhaba güncelleştirerek aygıtlarını devre dışı bırakabilir **durum** hello kimlik kayıt defterinde bir kimlik özelliği. Genellikle, iki senaryoda bu özelliği kullanın:

* Sağlama orchestration sürecinde. Daha fazla bilgi için bkz: [cihaz sağlamayı][lnk-guidance-provisioning].
* Kullanıyorsanız herhangi bir nedenle bir aygıt tehlikeye veya yetkisiz duruma geldi düşünün.

## <a name="import-and-export-device-identities"></a>İçeri ve dışarı aktarma aygıt kimlikleri

Cihaz kimliklerini toplu hello zaman uyumsuz işlemleri kullanarak bir IOT hub'ın kimlik kayıt defterinden dışarı aktarabilirsiniz [IOT hub'ı kaynak sağlayıcı uç][lnk-endpoints]. Dışarı aktarma uzun süre bir müşteri tarafından sağlanan blob kapsayıcı toosave aygıt kimlik verilerini kullanan işleri hello kimlik kayıt defterinden okunacak çalışan.

Merhaba zaman uyumsuz işlemleri kullanarak toplu tooan IOT hub'ın kimlik kayıt defterinde bir cihaz kimlikleri içeri aktarabilirsiniz [IOT hub'ı kaynak sağlayıcı uç][lnk-endpoints]. İçeri aktarmalar olan verileri bir müşteri tarafından sağlanan blob kapsayıcı toowrite aygıt kimlik verilerini hello kimlik kayıt defterine kullanmak uzun süre çalışan işleri.

* Merhaba içeri ve dışarı aktarma API'leri hakkında ayrıntılı bilgi için bkz: [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis].
* çalıştırma hakkında daha fazla bilgi almak ve işler dışarı bkz toolearn [toplu yönetim IOT Hub cihaz kimlikleri][lnk-bulk-identity].

## <a name="device-provisioning"></a>Cihaz sağlama

belirli bir IOT çözüm depolar hello cihaz verileri bu çözümün hello belirli gereksinimlerine bağlıdır. Ancak, en az bir çözüm cihaz kimliklerini ve kimlik doğrulama anahtarları depolamanız gerekir. Azure IOT Hub kimlikleri, kimlik doğrulama anahtarları ve durum kodları gibi her bir cihaz için değerler saklayabilirsiniz bir kimlik kayıt defterini içerir. Bir çözüm herhangi bir ek aygıt veri tablosu, blob depolama veya Cosmos DB toostore gibi diğer Azure hizmetleriyle kullanabilirsiniz.

*Cihaz sağlama* çözümünüzde hello ilk cihaz veri toohello depoları ekleme hello işlemidir. Yeni bir cihaz tooconnect tooyour hub tooenable, bir cihaz kimliği ve anahtarları toohello IOT Hub kimlik kayıt eklemeniz gerekir. Sağlama işlemi hello bir parçası olarak, diğer çözüm depolarında tooinitialize aygıta özgü veriler gerekebilir.

## <a name="device-heartbeat"></a>Cihaz sinyal

Merhaba IOT Hub kimlik kayıt defteri adlı bir alanı içeren **connectionState**. Yalnızca hello kullan **connectionState** geliştirme ve hata ayıklama sırasında alan. IOT çözümleri hello alanını çalışma zamanında sorgu değil. Örneğin, hello sorgulamaz **connectionState** bir bulut cihaz ileti veya SMS göndermeden önce bir aygıt bağlıysa, alan toocheck.

Bir aygıt bağlıysa, IOT çözümünüzü tooknow gerekirse, hello uygulamalıdır *sinyal düzeni*.

Merhaba sinyal desende hello aygıt en az bir kez her sabit süreyi (örneğin, en az bir kez her saat) cihaz bulut iletilerini gönderir. Bu nedenle, bir cihaz tüm verileri toosend sahip değilse, hala bir boş cihaz bulut iletisiyle (genellikle bir sinyal tanımlayan bir özellik) gönderir. Merhaba hizmet tarafında hello çözüm her cihaz için alınan son sinyal hello ile bir eşleme tutar. Merhaba çözüm hello aygıttan hello beklenen süre içinde bir sinyal iletisi almazsa, hello aygıtıyla ilgili bir sorun olduğunu varsayar.

Daha karmaşık bir uygulama hello bilgileri içerebilir [izleme işlemleri] [ lnk-devguide-opmon] tooconnect çalıştığınız veya iletişim tooidentify cihazlar ancak başarısız. Merhaba sinyal düzeni uyguladığınızda emin toocheck olun [IOT Hub kotaları ve kısıtlamaları][lnk-quotas].

> [!NOTE]
> Bir IOT çözüm kullanır hello bağlantısı olup yalnızca toodetermine durum varsa toosend bulut-cihaz iletilerini ve iletileri yayın aygıtları toolarge kümesi, hello daha basit kullanmayı *kısa süre sonu zamanı* düzeni. Bu desen hello daha verimli devam ederken hello sinyal desen kullanan bir cihaz bağlantı durumu kayıt Bakımı olarak aynı sonucu elde eder. IOT hub'ı ileti onayları isterse, hangi aygıtların mümkün tooreceive iletileri ve hangi değil hakkında bildirebilir.

## <a name="device-lifecycle-notifications"></a>Cihaz yaşam döngüsü bildirimleri

Bir cihaz kimliği oluşturulduğunda veya cihaz yaşam döngüsü bildirimleri göndererek silinmiş IOT hub'ı IOT çözümünüzü bildirebilir. toodo bu nedenle, IOT çözümünüzü toocreate bir yol ve tooset hello veri kaynağı eşittir çok gereken*DeviceLifecycleEvents*. Varsayılan olarak, hiçbir yaşam döngüsü bildirimleri gönderilir, diğer bir deyişle, bu tür bir yollar önceden mevcut. Merhaba bildirim iletisi özelliklerini ve gövde içerir.

Özellikler: İleti sistemi özellikleri ile Merhaba önek `'$'` simgesi.

| Ad | Değer |
| --- | --- |
$content-türü | uygulama/json |
$iothub-enqueuedtime |  Zaman zaman hello bildirim gönderildi |
$iothub-ileti-kaynak | deviceLifecycleEvents |
$content-kodlama | UTF-8 |
opType | **createDeviceIdentity** veya **deleteDeviceIdentity** |
hubName | IOT hub'ının adı |
deviceId | Merhaba aygıtın kimliği |
operationTimestamp | İşlemin ISO8601 zaman damgası |
ıothub ileti şeması | deviceLifecycleNotification |

Gövdesi: Bu bölümde JSON biçiminde ve cihaz kimliği oluşturdunuz Merhaba, hello twin temsil eder. Örneğin,

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>Başvuru konuları:

Merhaba aşağıdaki başvuru konuları hello kimlik kayıt defteri hakkında daha fazla bilgi sağlar.

## <a name="device-identity-properties"></a>Cihaz kimlik özellikleri

Cihaz kimliklerini JSON belgeleri olarak aşağıdaki özelliklere hello ile temsil edilir:

| Özellik | Seçenekler | Açıklama |
| --- | --- | --- |
| deviceId |gerekli, güncelleştirmelerinin salt okunur |(Yukarı too128 karakter uzunluğunda) büyük küçük harf duyarlı dize ASCII 7 bit alfasayısal karakter + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Generationıd |gerekli, salt okunur |Bir IOT hub tarafından üretilen, büyük küçük harf duyarlı dize too128 karakter uzunluğunda ayarlama. Merhaba kullanılan toodistinguish aygıtlarla bu değerdir aynı **DeviceID**, silinmiş ve yeniden oluşturulacak. |
| ETag |gerekli, salt okunur |Göre zayıf bir ETag hello cihaz kimliği için temsil eden bir dize [RFC7232][lnk-rfc7232]. |
| kimlik doğrulama |İsteğe bağlı |Kimlik doğrulama bilgileri ve güvenlik malzemeleri içeren bileşik bir nesne. |
| auth.symkey |İsteğe bağlı |Base64 biçiminde depolanan birincil ve ikincil bir anahtar içeren bileşik bir nesne. |
| durum |Gerekli |Bir erişim göstergesidir. Olabilir **etkin** veya **devre dışı**. Varsa **etkin**, hello aygıt tooconnect izin verilir. Varsa **devre dışı**, bu cihazı herhangi bir aygıt'e yönelik uç nokta erişemiyor. |
| statusReason |İsteğe bağlı |128 karakter uzunluğundaki hello aygıt kimlik durumu bu depoları hello nedenle dize. Tüm UTF-8 karakterlere izin verilir. |
| statusUpdateTime |Salt okunur |Başlangıç tarihi ve saati hello son durum güncelleştirmesi gösteren bir zamana bağlı göstergesi. |
| connectionState |Salt okunur |Bağlantı durumunu gösteren bir alan: ya da **bağlı** veya **bağlantı kesildi**. Bu alan hello hello cihaz bağlantı durumunun IOT Hub görünümünü temsil eder. **Önemli**: Bu alan yalnızca geliştirme/hata ayıklama amacıyla kullanılmalıdır. Merhaba bağlantı durumu yalnızca MQTT veya AMQP kullanarak aygıtlar için güncelleştirilmiştir. Ayrıca, protokol düzeyi ping (ping MQTT veya AMQP ping) dayalıdır ve yalnızca 5 dakika cinsinden bir maksimum gecikme olabilir. Bu nedenlerle, olabilir hatalı pozitif sonuç gibi cihazlar bağlı olarak bildirilen ancak, kesilir. |
| connectionStateUpdatedTime |Salt okunur |Başlangıç tarihini ve son zaman hello bağlantı durumu gösteren zamana bağlı bir gösterge güncelleştirildi. |
| lastActivityTime |Salt okunur |Başlangıç tarihini ve son zaman hello aygıt gösteren zamana bağlı bir göstergesi, bağlı, alınan veya gönderilen bir ileti. |

> [!NOTE]
> Bağlantı durumu yalnızca hello hello bağlantının hello durumunun IOT Hub görünümünü temsil edebilir. Ağ koşulları ve yapılandırmaları bağlı olarak güncelleştirmeleri toothis durumu gecikebilir.

## <a name="additional-reference-material"></a>Ek başvuru bilgileri

Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:

* [IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.
* [Azaltma ve kotaları] [ lnk-quotas] hello kotaları açıklar ve IOT Hub hizmeti toohello uygulamak davranışları azaltma.
* [Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.
* [IOT hub'ı sorgu dili] [ lnk-query] tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz hello sorgu dili açıklar.
* [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.

## <a name="next-steps"></a>Sonraki adımlar

Şimdi nasıl toouse hello IOT Hub kimlik kayıt defteri, IOT Hub Geliştirici Kılavuzu konuları aşağıdaki hello ilgilenebilirsiniz öğrendiniz:

* [Denetim erişim tooIoT Hub][lnk-devguide-security]
* [Cihaz çiftlerini toosynchronize durumu ve yapılandırmaları kullanacak][lnk-devguide-device-twins]
* [Bir cihazda doğrudan bir yöntem çağırma][lnk-devguide-directmethods]
* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticiyi izleyerek hello ilgilenen olabilir:

* [Azure IOT Hub ile çalışmaya başlama][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
