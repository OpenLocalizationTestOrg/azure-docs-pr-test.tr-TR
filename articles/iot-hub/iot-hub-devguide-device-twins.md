---
title: "aaaUnderstand Azure IOT Hub cihaz çiftlerini | Microsoft Docs"
description: "Geliştirici Kılavuzu - kullanım cihaz IOT Hub ve aygıtlarınızın arasında toosynchronize durumu ve yapılandırma verileri çiftlerini"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>Anlama ve IOT hub'da cihaz çiftlerini kullanın
## <a name="overview"></a>Genel Bakış
*Cihaz çiftlerini* aygıt durum bilgilerini (meta verileri, yapılandırmaları ve koşullar) depolamak JSON belgeleri. IOT Hub cihaz çifti tooIoT Hub bağlanmak her aygıt için devam ettirir. Bu makalede açıklanır:

* Merhaba hello cihaz çifti yapısını: *etiketleri*, *istenen* ve *özellikleri bildirilen*, ve
* cihaz çiftlerini cihaz uygulamalarını hem de arka uçları gerçekleştirebilirsiniz hello işlemleri.

> [!NOTE]
> Şu anda, cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak. Toohello başvuran [MQTT Destek] [ lnk-devguide-mqtt] hakkında yönergeler için makalenin tooconvert mevcut aygıt uygulama toouse MQTT.
> 
> 

### <a name="when-toouse"></a>Zaman toouse
Cihaz çiftlerini kullanın:

* Aygıta özgü meta veriler hello bulutta depolayın. Örneğin, bir satış makinenin dağıtım konumu hello.
* Rapor geçerli durumu bilgileri kullanılabilir özellikleri ve aygıt uygulamanızdan koşulları gibi. Örneğin, bir cihaz bağlı tooyour IOT hub, cep telefonu üzerinden veya WiFi.
* Uzun süre çalışan iş akışları cihaz uygulaması ve arka uç uygulaması arasında Hello durumunu eşitleyin. Örneğin, Hello çözüm yedeklediğinizde son yeni bellenim sürümü tooinstall hello ve hello cihaz uygulama raporları hello güncelleştirme işleminin çeşitli aşamaları hello belirtir.
* Cihaz meta verilerini, yapılandırma veya durumu sorgu.

Çok başvuran[cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] bildirilen özellikleri, cihaz bulut iletilerini veya karşıya dosya yükleme kullanma konusunda yönergeler için.
Çok başvuran[bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] istenen özellikler, doğrudan yöntemleri veya Bulut-cihaz iletilerini kullanma konusunda yönergeler için.

## <a name="device-twins"></a>Cihaz çiftlerini
Cihaz çiftlerini cihaz ile ilgili bilgileri depolar:

* Cihaz ve arka uç toosynchronize aygıt koşullar ve yapılandırma kullanabilirsiniz.
* Merhaba çözüm arka ucu tooquery ve uzun süre çalışan işlemleri hedef kullanabilirsiniz.

cihaz çifti Hello yaşam döngüsü bağlı toohello karşılık gelen [cihaz kimliği][lnk-identity]. Cihaz çiftlerini örtük olarak oluşturulur ve yeni bir cihaz kimliği oluşturulduğunda veya IOT hub'da silinmiş silinir.

Cihaz çifti içeren bir JSON belgesi şöyledir:

* **Etiketleri**. Çözüm arka ucu hello hello JSON belgesinin bir bölümünü okuma ve yazma. Etiketler görünür toodevice uygulamalar olup olmadığı.
* **Özellikler istenen**. Bildirilen özellikleri toosynchronize aygıt yapılandırması veya koşulları ile birlikte kullanılır. İstenen özellikler yalnızca hello çözüm tarafından arka uç ayarlayabilirsiniz ve hello cihaz uygulama tarafından okunabilir. Merhaba cihaz uygulaması, gerçek zamanlı istenen hello özelliklerindeki değişiklikler de bildirilebilir.
* **Özellikler bildirilen**. İstenen özelliklerde toosynchronize aygıt yapılandırması veya koşulları ile birlikte kullanılır. Bildirilen özellikleri yalnızca hello cihaz uygulama tarafından ayarlanabilir ve okunabilir ve hello çözüm arka ucu tarafından sorgulanan.

Ayrıca, hello salt okunur özellikler hello hello saklanan karşılık gelen cihaz Kimliği'hello hello cihaz çifti JSON belgesi kökündeki içeren [kimlik kayıt defteri][lnk-identity].

![][img-twin]

Aşağıdaki örnek hello cihaz çifti JSON belgesi gösterir:

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

Merhaba kök nesnesindeki hello sistem özelliklerdir ve kapsayıcı nesneleri için `tags` ve her ikisi de `reported` ve `desired` özellikleri. Merhaba `properties` kapsayıcısı bazı salt okunur öğeleri içerir (`$metadata`, `$etag`, ve `$version`) hello açıklanan [cihaz çifti meta verilerini] [ lnk-twin-metadata] ve [ İyimser eşzamanlılık] [ lnk-concurrency] bölümler.

### <a name="reported-property-example"></a>Bildirilen özelliği örneği
Merhaba önceki örnekte hello cihaz çifti içeren bir `batteryLevel` hello cihaz uygulaması tarafından bildirilen özelliği. Bu özellik, olası tooquery kolaylaştırır ve hello son bildirilen pil düzeyi temelinde cihazlarda çalışır. Merhaba cihaz uygulama raporlama cihaz özellikleri veya bağlantı seçenekleri diğer örnek olarak verilebilir.

> [!NOTE]
> Bildirilen özellikleri hello çözüm arka ucu bir özelliğin değerini bilinen son hello burada ilgilendiği senaryoları basitleştirin. Kullanım [cihaz bulut iletilerini] [ lnk-d2c] hello çözüm arka ucu tooprocess cihaz telemetrisi zaman serisi gibi zaman damgalı olaylar dizisini hello biçiminde gerekip gerekmediğini.

### <a name="desired-property-example"></a>İstenen özelliği örneği
Merhaba önceki örnekte hello `telemetryConfig` cihaz çifti istenen ve bildirilen özellikleri hello çözüm arka ucu ve hello aygıt uygulama toosynchronize hello telemetri yapılandırması tarafından bu aygıt için kullanılır. Örneğin:

1. Hello çözüm arka ucu istenen hello özelliğiyle istenen hello yapılandırma değeri ayarlar. İstenen hello özellik kümesi hello belgeyle hello kısmı şöyledir:
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. Merhaba cihaz uygulaması hemen bağlı veya hello ilk yeniden hello değişikliği bildirilir. Merhaba cihaz uygulamasının daha sonra güncelleştirilen hello yapılandırma raporlar (veya hello kullanarak bir hata koşulu `status` özelliği). İşte hello hello kısmı bildirilen özellikleri:
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. Merhaba çözüm arka ucu izleyebilirsiniz hello yapılandırma işlemi hello sonuçlarını birçok cihaz arasında göre [sorgulama] [ lnk-query] cihaz çiftlerini.

> [!NOTE]
> Merhaba önceki kod parçacıkları, örnekler bir aygıt yapılandırmasını ve durumunu bir yolu tooencode okunabilmesi için en iyi duruma getirilmiş. Merhaba cihaz çifti istenen ve hello cihaz çiftlerini özelliklerinde rapor için IOT hub'ı belirli bir şema getirmez.
> 
> 

Bellenim güncelleştirmeleri gibi çiftlerini toosynchronize uzun süre çalışan işlemleri kullanabilirsiniz. Nasıl bkz: toouse özellikleri toosynchronize ve cihazlarda, uzun süre çalışan işlemin izleme hakkında daha fazla bilgi için [kullanım istenen özellikleri tooconfigure aygıtları][lnk-twin-properties].

## <a name="back-end-operations"></a>Arka plan işlemleri
Merhaba çözüm arka ucu hello cihaz çifti atomik işlemleri, HTTP kullanıma sunulan aşağıdaki hello kullanarak çalıştırır:

1. **Cihaz çifti kimliğine göre almak**. Etiketler dahil ve istenen, hello cihaz çifti belge bildirilen, bu işlem döndürür ve Sistem Özellikleri.
2. **Cihaz çifti kısmen güncelleştirmek**. Bu işlem hello çözüm arka ucu toopartially güncelleştirme hello etiket veya cihaz çiftine istenen özellikler sağlar. Merhaba kısmi güncelleştirme ekler veya herhangi bir özellik güncelleştirmeleri bir JSON belgesi olarak ifade edilir. Çok ayarlanan özellikleri`null` kaldırılır. Merhaba aşağıdaki örnek yeni bir istenen özellik değeri ile oluşturur `{"newProperty": "newValue"}`, hello varolan değerini geçersiz kılar `existingProperty` ile `"otherNewValue"`ve kaldırır `otherOldProperty`. Başka değişiklik istenen tooexisting özellikleri veya etiketleri oluşturulur:
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **İstenen Özellikleri Değiştir**. Bu işlemi etkinleştirir hello çözüm arka ucu toocompletely tüm mevcut istenen özellikleri üzerine ve yeni bir JSON belgesi için alternatif `properties/desired`.
4. **Etiketleri değiştirmek**. Bu işlemi etkinleştirir hello çözüm arka ucu toocompletely tüm varolan etiketleri üzerine ve yeni bir JSON belgesi için alternatif `tags`.
5. **Twin bildirimlerin**. Bu işlem hello çözüm arka ucu toobe hello twin değiştirildiğinde bildirim sağlar. toodo bu nedenle, IOT çözümünüzü toocreate bir yol ve tooset hello veri kaynağı eşittir çok gereken*twinChangeEvents*. Varsayılan olarak, hiçbir twin bildirimler gönderilir, diğer bir deyişle, bu tür bir yollar önceden mevcut. Merhaba değişme oranı çok yüksek ise veya iç hataları gibi başka bir nedenle hello IOT hub'ı tüm değişiklikleri içeren tek bir bildirim gönderebilirsiniz. Uygulamanızı güvenilir denetim ve tüm ara durumlarıyla ilgili günlük gerekiyorsa, bu nedenle, daha sonra hala D2C iletileri kullanan önerilir. Merhaba twin bildirim iletisi özelliklerini ve gövde içerir.

    - Özellikler

    | Ad | Değer |
    | --- | --- |
    $content-türü | uygulama/json |
    $iothub-enqueuedtime |  Zaman zaman hello bildirim gönderildi |
    $iothub-ileti-kaynak | twinChangeEvents |
    $content-kodlama | UTF-8 |
    deviceId | Merhaba aygıtın kimliği |
    hubName | IOT hub'ının adı |
    operationTimestamp | [ISO8601] işleminin zaman damgası |
    ıothub ileti şeması | deviceLifecycleNotification |
    opType | "replaceTwin" veya "updateTwin" |

    İleti sistemi özellikleri ile Merhaba önekli `'$'` simgesi.

    - Gövde
        
    Bu bölüm bir JSON biçiminde tüm hello twin değişiklikleri içerir. Bir düzeltme eki hello aynı biçimi kullanır, hello farkı olan tüm twin bölümleri içerebilir: etiketleri, properties.reported, properties.desired ve hello "$metadata" öğeleri içerir. Örneğin,
    ```
    {
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

Tüm önceki operations desteği hello [iyimser eşzamanlılık] [ lnk-concurrency] ve hello gerektiren **ServiceConnect** hello tanımlanan izin [güvenlik ] [ lnk-security] makalesi.

Ayrıca son can toothese işlemleri, hello çözüm arka:

* Sorgu hello kullanarak hello cihaz çiftlerini SQL benzeri [IOT hub'ı sorgu dili][lnk-query].
* Büyük kümelerini kullanarak cihaz çiftlerini işlemleri [işleri][lnk-jobs].

## <a name="device-operations"></a>Aygıt işlemleri
Merhaba cihaz uygulaması atomik işlemleri aşağıdaki hello kullanarak hello cihaz çifti üzerinde çalışır:

1. **Cihaz çifti almak**. Bu işlem hello cihaz çifti belgeyi döndürür (etiketler dahil ve istenen, rapor ve Sistem Özellikleri) hello cihaz şu anda bağlı.
2. **Kısmen bildirilen özellikleri güncelleştirmek**. Bu işlemi etkinleştirir hello kısmi güncelleştirilmesini hello hello şu anda bağlı cihaz özelliklerini bildirdi. Aynı JSON güncelleştirme bu işlemi kullanan hello hello çözüm arka uç kullanan istenen özelliklerinin kısmi bir güncelleştirme için biçimlendirin.
3. **İstenen özelliklerde gözlemlemek**. Merhaba şu anda bağlı cihaz gerçekleşmeden güncelleştirmeleri istenen toohello özelliklerini bildirim toobe seçebilirsiniz. Merhaba aygıt güncelleştirme (kısmi veya tam değiştirme) aynı biçiminde hello çözüm arka ucu tarafından yürütülen hello alır.

Tüm önceki işlemleri hello hello gerektiren **DeviceConnect** hello tanımlanan izin [güvenlik] [ lnk-security] makalesi.

Merhaba [Azure IOT cihaz SDK'ları] [ lnk-sdks] birçok diller ve platformlar işlemlerinden önceki kolay toouse hello kolaylaştırır. İstenen özelliklerde eşitleme için IOT hub'ı elemanlar hello ayrıntıları hakkında daha fazla bilgi bulunabilir [aygıt yeniden bağlanmayı akış][lnk-reconnection].

> [!NOTE]
> Şu anda, cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak.
> 
> 

## <a name="reference-topics"></a>Başvuru konuları:
Merhaba aşağıdaki başvuru konuları denetleme erişim tooyour IOT hub'ı hakkında daha fazla bilgi sağlar.

## <a name="tags-and-properties-format"></a>Etiketleri ve özellikleri biçimi
Etiketler, istenen ve bildirilen özellikleri hello kısıtlamaları aşağıdaki JSON nesneleridir:

* JSON nesnelerinin tüm anahtarları büyük küçük harfe duyarlı 64 baytı UTF-8 UNICODE dizeleri içindedir. Karakter hariç UNICODE denetim karakterleri (kesimleri C0 ve C1) izin verilen ve `'.'`, `' '`, ve `'$'`.
* JSON nesnelerinin tüm değerleri şu JSON türlerini hello olabilir: boolean, sayı, dize, nesne. Diziler izin verilmiyor.
* Etiketler, istenen ve bildirilen özellikleri tüm JSON nesnelerinin maksimum derinliği 5 olabilir. Örneğin, nesne aşağıdaki hello geçerlidir:

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* Tüm dize değerleri en fazla uzunluk olarak 512 baytlık olabilir.

## <a name="device-twin-size"></a>Cihaz çifti boyutu
IOT hub'ı zorlayan bir 8KB boyutu sınırlaması hello değerleri `tags`, `properties/desired`, ve `properties/reported`, salt okunur öğeleri hariç.
Merhaba boyutu sayım tarafından UNICODE hariç tüm karakter denetim karakterleri (kesimleri C0 ve C1) ve alan hesaplanır `' '` dışında bir dize sabiti olduğunda görünür.
IOT hub'ı bir hata ile bu belgelerin hello sınırı üstünde hello boyutunu artırır tüm işlemleri reddeder.

## <a name="device-twin-metadata"></a>Cihaz çifti meta veriler
IOT Hub cihaz çifti her JSON nesnesinde son güncelleştirmesi hello hello zaman damgası istenen ve Özellikler bildirilen korur. Merhaba zaman damgaları UTC biçimindedir ve hello kodlanmış [ISO8601] biçimi `YYYY-MM-DDTHH:MM:SS.mmmZ`.
Örneğin:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Bu bilgiler Nesne anahtarları kaldıran her düzey (Merhaba JSON yapısı, yalnızca hello bırakır) toopreserve güncelleştirmeleri tutulur.

## <a name="optimistic-concurrency"></a>İyimser eşzamanlılık
Etiketler, istenen ve tüm destek iyimser eşzamanlılık özellikleri bildirdi.
Etiketler göre bir ETag sahip [RFC7232], hello etiketinin JSON gösterimi temsil eden. Etag'ler hello çözüm arka ucu tooensure tutarlılık koşullu güncelleştirme işlemlerini kullanabilirsiniz.

Cihaz çifti istenen ve Özellikler rapor Etag'ler gerekmez, ancak sahip bir `$version` toobe artımlı garanti değeri. Benzer şekilde tooan ETag, hello sürüm güncelleştirmelerini taraf tooenforce tutarlılığı güncelleştirme hello tarafından kullanılabilir. Örneğin, bir cihaz uygulaması için bir bildirilen özelliği veya hello çözüm arka ucu istenen bir özellik için.

Bir gözlemci Aracı (örneğin, istenen hello özellikleri Gözlemleme hello cihaz uygulaması) alma işleminin hello sonucu bir güncelleştirme bildirimi arasındaki diğerleriyle mutabık kılmak sürümleri de yararlı olur. Merhaba bölüm [aygıt yeniden bağlanmayı akış] [ lnk-reconnection] daha fazla bilgi sağlar.

## <a name="device-reconnection-flow"></a>Cihaz yeniden bağlanmayı akışı
IOT Hub bağlantısı kesilmiş aygıtları için istenen özellikler güncelleştirme bildirimlerini korumaz. Bu güncelleştirme bildirimlerini toplama toosubscribing de hello tam istenen özellikler belgesinde bağlanan bir aygıt almanız gerekir izler. Güncelleştirme bildirimlerini ve tam alma arasında diğerleriyle Hello olasılığını göz önüne alındığında, akış aşağıdaki hello güvence altına gerekir:

1. Cihaz uygulaması tooan IOT hub'ı bağlar.
2. Cihaz uygulaması istenen özelliklerini güncelleştirme bildirimlerini abone olur.
3. Cihaz uygulaması hello tam belge istenen özellikleri alır.

Merhaba cihaz uygulaması ile tüm bildirimleri yoksayabilirsiniz `$version` hello tam alınan belge hello sürümünden eşit veya daha az. Bu yaklaşım olası nedeni IOT hub'ı sürümleri her zaman artırmak güvence altına alır.

> [!NOTE]
> Bu mantık hello zaten uygulanmış [Azure IOT cihaz SDK'ları][lnk-sdks]. Bu açıklama hello cihaz uygulaması Azure IOT cihaz SDK'ları hiçbirini kullanamazsınız ve hello MQTT arabirimi doğrudan program gerekir yararlıdır.
> 
> 

## <a name="additional-reference-material"></a>Ek başvuru bilgileri
Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:

* Merhaba [IOT Hub uç noktaları] [ lnk-endpoints] makalede hello çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları.
* Merhaba [azaltma ve kotaları] [ lnk-quotas] makale toohello IOT Hub hizmetine uygulamak ve hello hizmetini kullandığınızda azaltma davranışı tooexpect hello hello kotaları açıklar.
* Merhaba [Azure IOT SDK'ları cihazını ve hizmetini] [ lnk-sdks] makale listeleri hello çeşitli dil SDK'lar, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.
* Merhaba [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] makalede hello tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz IOT hub'ı sorgulama dili .
* Merhaba [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] makale hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Cihaz çiftlerini hakkında öğrendiniz artık IOT Hub Geliştirici Kılavuzu konuları aşağıdaki hello ilgilenen olabilir:

* [Bir cihazda doğrudan bir yöntem çağırma][lnk-methods]
* [Birden çok aygıta işleri zamanla][lnk-jobs]

Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticileri aşağıdaki hello ilgilenen olabilir:

* [Nasıl toouse hello cihaz çifti][lnk-twin-tutorial]
* [Nasıl toouse cihaz çifti özellikleri][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
