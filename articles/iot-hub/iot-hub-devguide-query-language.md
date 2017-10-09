---
title: aaaUnderstand hello Azure IOT Hub sorgu dili | Microsoft Docs
description: "Geliştirici Kılavuzu - hello SQL benzeri IOT hub'ı sorgu dili açıklaması cihaz çiftlerini ve IOT hub'ınızı işlerden hakkında tooretrieve bilgi kullanılır."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Başvuru - cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili

IOT hub'ı güçlü SQL benzeri bir dil tooretrieve bilgilerini sağlamaktadır ilgili [cihaz çiftlerini] [ lnk-twins] ve [işleri][lnk-jobs]ve [ileti yönlendirme][lnk-devguide-messaging-routes]. Bu makalede sunar:

* Bir giriş toohello ana özelliklerini hello IOT hub'ı sorgu dili ve
* Merhaba hello dil açıklaması ayrıntılı.

## <a name="get-started-with-device-twin-queries"></a>Cihaz çifti sorguları ile çalışmaya başlama
[Cihaz çiftlerini] [ lnk-twins] etiketleri ve özellikleri rastgele JSON nesnelerini içerebilir. IOT Hub, tooquery cihaz çiftlerini tüm cihaz çifti bilgilerini içeren tek bir JSON belgesi olarak sağlar.
Örneğin, IOT hub cihaz çiftlerini yapı izlenerek hello olduğunu varsayın:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IOT hub'ı sunan hello cihaz çiftlerini adlı bir belge koleksiyonu olarak **aygıtları**.
Bu nedenle sorgu aşağıdaki hello hello tüm cihaz çiftlerini kümesini alır:

```sql
SELECT * FROM devices
```

> [!NOTE]
> [Azure IOT SDK'ları] [ lnk-hub-sdks] büyük sonuçlarının disk belleği destekler.

IOT Hub ile rastgele koşullar filtreleme tooretrieve cihaz çiftlerini sağlar. Örneğin,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

alır hello cihaz çiftlerini ile Merhaba **location.region** etiketi ayarlayın çok**ABD**.
Boole işleçleri ve aritmetik karşılaştırmaları de, örneğin desteklenir

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

Merhaba BİZE yapılandırılmış toosend telemetri değerinden genellikle dakikada bulunan tüm cihaz çiftlerini alır. Kolaylık, aynı zamanda hello ile olası toouse dizi sabitleri olup **IN** ve **NBU** (içinde değil) işleçler. Örneğin,

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

WiFi bildirilen veya bağlantı kablolu tüm cihaz çiftlerini alır. Bu genellikle gerekli tooidentify belirli bir özellik içeren tüm cihaz çiftlerini değil. IOT hub'ı destekleyen hello işlevi `is_defined()` bu amaç için. Örneğin,

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

Merhaba tanımlamak tüm cihaz çiftlerini alınan `connectivity` özelliği bildirdi. Toohello başvuran [WHERE yan tümcesi] [ lnk-query-where] filtreleme özellikleri hello hello tam başvuru için bölüm.

Gruplandırma ve toplamalar da desteklenir. Örneğin,

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Merhaba cihaz Hello sayısı her telemetri yapılandırma durumunu döndürür.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Merhaba önceki örnekte burada üç aygıt başarılı bir yapılandırma bildirilen, iki hala hello yapılandırmayı uygulama ve bir hata bildirdi bir durum gösterilir.

### <a name="c-example"></a>C# örnek
Merhaba sorgu işlevi hello tarafından sunulan [C# hizmeti SDK'sını] [ lnk-hub-sdks] hello içinde **RegistryManager** sınıfı.
Burada, basit bir sorgu örneği verilmiştir:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Not nasıl hello **sorgu** nesne örneği içeren bir sayfa boyutuna (yukarı too1000) ve ardından birden çok sayfa arama hello tarafından alınabilecek **GetNextAsTwinAsync** yöntemleri birden çok kez.
Bu hello sorgu nesneyi kullanıma sunan birden çok Not **sonraki\***, cihaz çifti ya da iş nesneleri gibi hello sorgu gerektirdiği hello seri durumdan çıkarma seçeneği veya tahminleri kullanılırken düz JSON toobe bağlı olarak.

### <a name="nodejs-example"></a>Node.js örneği
Merhaba sorgu işlevi hello tarafından sunulan [Node.js için Azure IOT hizmeti SDK'sını] [ lnk-hub-sdks] hello içinde **kayıt defteri** nesnesi.
Burada, basit bir sorgu örneği verilmiştir:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Not nasıl hello **sorgu** nesne örneği içeren bir sayfa boyutuna (yukarı too1000) ve ardından birden çok sayfa arama hello tarafından alınabilecek **nextAsTwin** yöntemleri birden çok kez.
Bu hello sorgu nesneyi kullanıma sunan birden çok Not **sonraki\***, cihaz çifti ya da iş nesneleri gibi hello sorgu gerektirdiği hello seri durumdan çıkarma seçeneği veya tahminleri kullanılırken düz JSON toobe bağlı olarak.

### <a name="limitations"></a>Sınırlamalar
> [!IMPORTANT]
> Sorgu sonuçları gecikme saygı toohello en son değerleri ile birkaç dakika içinde cihaz çiftlerini olabilir. Tek tek cihaz çiftlerini kimliğine göre sorgulama, her zaman tercih toouse hello varsa, her zaman hello en son değerleri içerir ve daha yüksek azaltma sınırları cihaz çifti API alın.

Şu anda karşılaştırmaları yalnızca ilkel türler arasında (hiçbir nesne), örneğin desteklenir `... WHERE properties.desired.config = properties.reported.config` yalnızca bu özellikleri ilkel değerler varsa desteklenir.

## <a name="get-started-with-jobs-queries"></a>İşlerini sorguları ile çalışmaya başlama
[İşlerini] [ lnk-jobs] şekilde tooexecute aygıtları kümesi üzerinde işlemler sağlar. Her cihaz çifti onu olduğu adlı bir koleksiyon bölümünde hello işleri hello bilgileri içeren **işleri**.
Mantıksal olarak

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Bu koleksiyon şu anda olarak sorgulanabilir **devices.jobs** hello IOT hub'ı sorgu dili içinde.

> [!IMPORTANT]
> Şu anda hello işleri özelliği, hiçbir zaman cihaz çiftlerini (diğer bir deyişle, 'aygıtlardan' içeren sorgular) sorgulanırken döndürülür. Yalnızca doğrudan sorgu kullanarak erişilebilir `FROM devices.jobs`.
>
>

Örneğin, tooget tek bir cihazı etkileyen tüm işleri (Geçmiş ve zamanlanmış), sorgu aşağıdaki hello kullanabilirsiniz:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Bu sorgu hello cihaza özel durumu (ve büyük olasılıkla hello doğrudan yöntemi yanıtı) döndürülen her bir iş nasıl sağladığını unutmayın.
Aynı zamanda tüm nesne özellikleri hello içinde rastgele Boolean koşullarla olası toofilter olan **devices.jobs** koleksiyonu.
Örneğin, sorgu hello:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

Tüm tamamlanan alır cihaz çifti güncelleştirme işleri aygıtın **myDeviceId** Eylül 2016 sonra oluşturulmuş.

Ayrıca olası tooretrieve hello aygıt başına sonuçlarını tek bir işi yerdir.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Sınırlamalar
Üzerinde şu anda sorgular **devices.jobs** desteklemez:

* Projeksiyonlar, bu nedenle yalnızca `SELECT *` mümkündür.
* Toplama toojob özellikleri (önceki bölümde hello bakın) toohello cihaz çiftine başvuran koşulları.
* Count, avg, grupla gibi toplamalar gerçekleştiriliyor.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Cihaz bulut ileti yollar sorgu ifadeleri ile çalışmaya başlama

Kullanarak [cihaz bulut yolları][lnk-devguide-messaging-routes], IOT Hub'ın toodispatch cihaz-bulut iletileri karşı tek bir ileti hesaplanan ifadeleri göre toodifferent uç noktalarını yapılandırabilirsiniz.

Merhaba rota [koşulu] [ lnk-query-expressions] hello aynı IOT hub'ı sorgu dili twin ve iş sorguları koşullarında olarak kullanır. Yol koşulları hello ileti üstbilgilerini ve gövde değerlendirilir. Yönlendirme sorgu ifadesi yalnızca hello ileti gövdesi, yalnızca ileti üstbilgilerini gerektirebilir veya her ikisi de üstbilgileri iletisi ve ileti gövdesi. IOT hub'ı hello üstbilgiler ve ileti gövdesini sipariş tooroute iletileri için belirli bir şema olduğu varsayılır ve IOT hub'ı tooproperly rotası için gerekli olan bölümleri aşağıdaki hello açıklanmaktadır:

### <a name="routing-on-message-headers"></a>İleti üstbilgilerinde yönlendirme

IOT hub'ı ileti yönlendirme için ileti üstbilgilerini JSON gösterimi aşağıdaki hello varsayılır:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

İleti sistemi özellikleri ile Merhaba önekli `'$'` simgesi.
Kullanıcı özellikleri her zaman kendi adıyla erişilir. Bir kullanıcı özellik adı bir sistem özelliğiyle toocoincide ortaya çıkarsa (gibi `$to`), hello kullanıcı özelliği ile Merhaba alınan `$to` ifade.
Köşeli ayraçlar kullanan hello sistem özellik her zaman erişebilirsiniz `{}`: hello ifade örneği için kullanabileceğiniz `{$to}` tooaccess hello sistem özelliği `to`. Köşeli parantez içindeki özellik adları daima hello karşılık gelen sistem özelliği alır.

Özellik adları büyük küçük harfe duyarlı olduğunu unutmayın.

> [!NOTE]
> Tüm ileti özellikleri dizelerdir. Hello açıklandığı gibi sistem özelliklerini [Geliştirici Kılavuzu][lnk-devguide-messaging-format], şu anda kullanılabilir toouse sorgularda değildir.
>

Örneğin, kullanırsanız, bir `messageType` özelliği, tüm telemetri tooone endpoint ve tüm uyarıları tooanother uç tooroute isteyebilirsiniz. İfade tooroute hello telemetri aşağıdaki hello yazabilirsiniz:

```sql
messageType = 'telemetry'
```

Ve ifade tooroute hello uyarı iletileri hello aşağıdaki:

```sql
messageType = 'alert'
```

Boole ifadeleri ve işlevleri de desteklenir. Bu özellik, toodistinguish önem düzeyi arasında örneğin sağlar:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Toohello başvuran [ifade ve koşullar] [ lnk-query-expressions] bölümünü hello tam listesi için desteklenen işleçleri ve işlevleri.

### <a name="routing-on-message-bodies"></a>İleti gövdeleri yönlendirme

IOT Hub, ileti gövdesinde dayalı yalnızca yönlendirebilirsiniz hello ileti gövdesi doğru ise, içeriği biçimlendirilmiş JSON UTF-8, UTF-16 veya UTF-32 kodlanmış. Merhaba iletisinin hello içerik türü çok ayarlamalısınız`application/json` ve hello içerik kodlama tooone Merhaba, IOT hub'ı tooroute selamlama iletisine hello gövde içeriğine göre hello ileti üstbilgilerini tooallow UTF Kodlamalar desteklenir. Merhaba üstbilgileri birini belirtilmezse, IOT hub'ı hello gövde selamlama iletisine karşı içeren herhangi bir sorgu ifade tooevaluate denemez. İleti bir JSON ileti değilse veya selamlama iletisine hello içerik türü ve içerik kodlamasını belirtmiyorsa, ileti tooroute selamlama iletisine hello ileti üstbilgilerinde tabanlı yönlendirme hala kullanabilir.

Kullanabileceğiniz `$body` hello sorgu ifadesi tooroute Başlangıç iletisi. Basit gövde başvurusu, gövde dizi başvuru ya da birden fazla gövde başvuru hello sorgu ifadesinde kullanabilirsiniz. Sorgu ifadesi ayrıca gövde başvuru iletisi başlığı başvurusu ile birleştirebilirsiniz. Örneğin, tüm geçerli sorgu ifadeleri hello şunlardır:

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>IOT Hub sorgusuyla temelleri
Her IOT hub'ı sorgu seçme ve FROM yan tümcesi ve isteğe bağlı WHERE ve GROUP BY yan tümceleri oluşur. Her sorgu JSON belgeleri, örneğin cihaz çiftlerini topluluğu üzerinde çalıştırılır. Merhaba FROM yan tümcesi üzerinde yinelendiğinde hello belge koleksiyonu toobe gösterir (**aygıtları** veya **devices.jobs**). Ardından, burada yan tümcesi uygulanır hello filtrede hello. Toplamalar ile bu adımı hello sonuçlarını GROUP BY yan tümcesi içinde belirtilen hello gruplandırılır ve her grup için bir satır oluşturulur hello SELECT yan tümcesinde belirtilen.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>FROM yan tümcesi
Merhaba **< from_specification > gelen** yan tümcesi, yalnızca iki değer varsayabilirsiniz: **AYGITLARDAN**, tooquery cihaz çiftlerini veya **devices.jobs gelen**, tooquery işi cihaz başına Ayrıntıları.

## <a name="where-clause"></a>WHERE yan tümcesi
Merhaba **burada < filter_condition >** yan tümcesi isteğe bağlıdır. Merhaba JSON belgelerini hello FROM koleksiyonundaki hello sonuç bir parçası olarak dahil edilen toobe getirmelidir bir veya daha fazla koşulları belirtir. Herhangi bir JSON belge değerlendirilmelidir hello belirtilen koşullar çok "true" Merhaba sonucunda içerilen toobe.

Merhaba izin koşulları bölümünde açıklanan [ifadeleri ve koşullar][lnk-query-expressions].

## <a name="select-clause"></a>SELECT yan tümcesi
Merhaba SELECT yan tümcesi (**seçin < select_list >**) zorunludur ve hangi değerlerin hello sorgudan alınan belirtir. Merhaba JSON değerleri toobe toogenerate yeni JSON nesnelerinin kullanılan belirtir.
Her öğe için filtrelenmiş (ve isteğe bağlı olarak gruplandırılmış) alt hello FROM koleksiyonunun Merhaba, hello projeksiyon aşaması hello SELECT yan tümcesinde belirtilen hello değerlerle oluşturulan yeni bir JSON nesnesi oluşturur.

Merhaba SELECT yan tümcesi hello dilbilgisi aşağıdadır:

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

Burada **attribute_name** tooany özelliği hello JSON belgesinin hello FROM koleksiyonundaki başvurur. SELECT yan tümceleri bazı örnekleri hello bulunabilir [cihaz çifti sorguları ile çalışmaya başlama] [ lnk-query-getstarted] bölümü.

Şu anda, seçim yan tümceleri farklı **seçin \***  cihaz çiftlerini toplama sorgularında yalnızca desteklenir.

## <a name="group-by-clause"></a>GROUP BY yan tümcesi
Merhaba **GROUP BY < group_specification >** yan tümcesi hello filtre hello WHERE yan tümcesinde belirtilen sonra çalıştırılabilir ve hello belirtilen hello projeksiyon önce seçin isteğe bağlı bir adım olan. Belgeleri bir özniteliğin hello değere göre gruplandırır. Bu gruplar, hello SELECT yan tümcesinde belirtilen toplanan kullanılan toogenerate değerlerdir.

GROUP BY kullanarak bir sorgu örneğidir:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Merhaba resmi için GROUP BY söz dizimi:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

Burada **attribute_name** tooany özelliği hello JSON belgesinin hello FROM koleksiyonundaki başvurur.

Şu anda hello GROUP BY yan tümcesi, yalnızca cihaz çiftlerini sorgulanırken desteklenir.

## <a name="expressions-and-conditions"></a>İfadeler ve koşullar
Yüksek bir düzeyde bir *ifade*:

* Bir JSON türü (örneğin, Boolean, sayı, dize, dizi veya nesne), tooan örneği değerlendirir ve
* Merhaba aygıt JSON belgesi ve yerleşik işleçler ve işlevleri kullanarak sabitleri gelen veri düzenleme tarafından tanımlanır.

*Koşullar* tooa Boolean değerlendirmek ifadeler. Boolean farklı herhangi sabiti **true** olarak kabul **false** (dahil olmak üzere **null**, **tanımsız**, tüm nesne veya dizi örneği Tüm dize ve açıkça hello Boolean **false**).

ifadeler Hello sözdizimi şöyledir:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

Burada:

| Simgesi | Tanım |
| --- | --- |
| attribute_name | Merhaba hello JSON belgesinde herhangi bir özelliği **FROM** koleksiyonu. |
| binary_operator | Herhangi bir ikili işleç listelenen hello [işleçleri](#operators) bölümü. |
| işlev_adı| Herhangi bir işlev listelenen hello [işlevleri](#functions) bölümü. |
| decimal_literal |Bir kayan noktalı ondalık gösterimde. |
| hexadecimal_literal |Bir sayı '0 x onaltılık basamak dizesiyle ve ardından' hello dizesiyle ifade. |
| string_literal |Dize değişmez değerleri, sıfır veya daha fazla Unicode karakter dizisi veya kaçış sıraları tarafından temsil edilen Unicode dizelerdir. Dize değişmez değerleri tek tırnak içine alınmış (kesme işareti: ') veya çift tırnak (tırnak işareti: "). Çıkışları izin: `\'`, `\"`, `\\`, `\uXXXX` 4 onaltılık basamak tarafından tanımlanan Unicode karakterler. |

### <a name="operators"></a>İşleçler
işleçler aşağıdaki hello desteklenir:

| Ailesi | İşleçler |
| --- | --- |
| Aritmetik |+,-,*,/,% |
| Mantıksal |VE VEYA DEĞİL |
| Karşılaştırma |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>İşlevler
Yalnızca desteklenen çiftlerini ve işleri hello sorgulanırken işlevi şu şekildedir:

| İşlevi | Açıklama |
| -------- | ----------- |
| IS_DEFINED(Property) | Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür (de dahil olmak üzere `null`). |

Yollar koşullarında matematik işlevleri aşağıdaki hello desteklenir:

| İşlevi | Açıklama |
| -------- | ----------- |
| Abs(x) | Sayısal ifade döndürür hello mutlak (pozitif) değerini hello belirtildi. |
| EXP(x) | Merhaba, hello üstel değer döndüren belirtilen sayısal ifade (e ^ x). |
| Power(x,y) | Döndürür hello belirtilen başlangıç değeri ifadesi toohello belirtilen güç (x ^ y).|
| SQUARE(x) | Merhaba kare döndürür hello sayısal değer belirtildi. |
| CEILING(x) | En küçük tamsayı değeri büyük hello veya belirtilen sayısal ifade hello eşit verir. |
| FLOOR(x) | Daha az Hello en büyük tamsayıyı döndürür veya bu değere eşit toohello sayısal ifade belirtildi. |
| SIGN(x) | Artı (+ 1), sıfır (0), döndürür hello veya sayısal ifade hello eksi (-1) belirtisi belirtildi.|
| Sqrt(x) | Merhaba kare döndürür hello sayısal değer belirtildi. |

Yollar koşullarında denetleme ve işlevleri atama türü aşağıdaki hello desteklenir:

| İşlevi | Açıklama |
| -------- | ----------- |
| AS_NUMBER | Merhaba giriş dizesi tooa sayıyı dönüştürür. `noop`Giriş bir sayı ise; `Undefined` dize bir sayıyı temsil etmiyor durumunda.|
| IS_ARRAY | Bir dizidir hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür. |
| IS_BOOL | Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir Boole değeri döndürür. |
| IS_DEFINED | Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür. |
| IS_NULL | Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri null döndürür. |
| IS_NUMBER | Bir sayıdır hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür. |
| IS_OBJECT | Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir JSON nesnesi döndürür. |
| IS_PRIMITIVE | Merhaba Hello türü ifade ilkel belirtilirse, gösteren bir Boole değeri döndürür (dize, Boolean, sayısal veya `null`). |
| IS_STRING | Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri bir dize verir. |

Yollar koşullarında dize işlevleri aşağıdaki hello desteklenir:

| İşlevi | Açıklama |
| -------- | ----------- |
| CONCAT(x,...) | İki veya daha fazla dize değerlerini birleştirme hello sonucu olan bir dize döndürür. |
| LENGTH(x) | Dize ifadesi belirtilen döndürür hello hello karakter sayısı.|
| Lower(x) | Büyük harf karakter veri toolowercase dönüştürmeden sonra bir dize ifadesi döndürür. |
| Upper(x) | Küçük harf karakter veri toouppercase dönüştürmeden sonra bir dize ifadesi döndürür. |
| SUBSTRING (dize, başlangıç [, uzunluk]) | Merhaba başlayan bir dize ifadesi döndürür parçası karakter sıfır tabanlı konumu belirtilen ve uzunluk veya hello dize toohello sonu toohello belirtilen devam eder. |
| INDEX_OF (dize, parça) | Merhaba dize bulunmazsa hello ikinci dize ifadesi hello ilk belirtilen dize ifadesi veya -1 içinde hello ilk oluşum konumunu başlangıç hello döndürür.|
| STARTS_WITH (x, y) | Merhaba ilk dize ifadesi ile Merhaba ikinci başlayıp başlamadığını gösteren bir Boole değeri döndürür. |
| ENDS_WITH (x, y) | Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür. |
| CONTAINS(x,y) | Merhaba ilk dize ifadesi hello ikinci içerip içermediğini gösteren bir Boole değeri döndürür. |

## <a name="next-steps"></a>Sonraki adımlar
Tooexecute kullanarak uygulamalarınızı nasıl sorgular öğrenin [Azure IOT SDK'ları][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
