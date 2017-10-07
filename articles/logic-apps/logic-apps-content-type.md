---
title: "aaaHandle içerik türleri - Azure Logic Apps | Microsoft Docs"
description: "Azure mantıksal uygulamaları tasarım ve çalışma zamanı içerik türleri ile nasıl ilgileneceğini"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a>Logic apps içinde içerik türlerini yönetmek

Farklı türlerde içerik JSON, XML, düz dosyalar ve ikili veriler dahil olmak üzere bir mantıksal uygulama akabilir. Merhaba Logic Apps altyapısı tüm içerik türlerini destekler, ancak bazı yerel hello Logic Apps altyapısı tarafından anlaşılır. Başkalarının atama veya dönüştürmeler gerektiğinde gerektirebilir. Bu makalede hello altyapısı farklı içerik türlerini nasıl işlediğini ve nasıl toocorrectly ele gerektiğinde bu türleri açıklanmaktadır.

## <a name="content-type-header"></a>Content-Type üstbilgisi

toostart temel olarak bakalım iki hello `Content-Types` yok gerektiren dönüştürme veya bir mantıksal uygulama kullanabileceğiniz atama: `application/json` ve `text/plain`.

## <a name="applicationjson"></a>Application/JSON

Merhaba iş akışı altyapısı kullanır hello üzerinde `Content-Type` HTTP başlığından toodetermine hello uygun işleme çağırır. Merhaba içerik türü herhangi bir istekle `application/json` depolanır ve bir JSON nesnesi olarak işlenir. Ayrıca, herhangi bir atama gerek kalmadan JSON içeriği, varsayılan olarak'e ayrıştırılabilir. 

Örneğin, hello içerik türü üstbilgisi bir istek ayrıştırılamıyor `application/json ` gibi bir ifade kullanarak bir iş akışında `@body('myAction')['foo'][0]` tooget hello değeri `bar` bu durumda:

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

Hiçbir ek atama gereklidir. JSON ancak belirtilen üstbilgi olmadığına verileri ile çalışıyorsanız, el ile hello kullanarak tooJSON çevirebilirsiniz `@json()` işlev, örneğin: `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Şema ve şema Oluşturucusu

Merhaba isteği tetikleyici tooenter JSON şeması sağlar tooreceive beklediğiniz için hello yükü. Bu şemayı hello isteği Merhaba içeriğine tüketebileceği şekilde belirteçleri oluşturmak hello designer sağlar. Bir şema hazır yoksa seçin **kullanım örnek yükü toogenerate şeması**, bir örnek yükü JSON şeması oluşturabilirsiniz.

![Şema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>'Parse JSON' eylemi

Merhaba `Parse JSON` eylem mantığı uygulama tüketimi için kolay belirteçler içine JSON içeriği ayrıştırılamıyor olanak sağlar. Benzer toohello isteği tetikleyici, bu eylem, girin ya da hello tooparse istediğiniz içerik için JSON şeması oluşturma sağlar. Bu araç Süren veri Service Bus, Azure Cosmos DB ve vb. kolaylaştırır.

![JSON ayrıştırılamıyor](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>Metin/düz

Benzer çok`application/json`, hello ile alınan HTTP iletisi `Content-Type` üstbilgisinin `text/plain` ham biçiminde depolanır. Bu ileti sonraki eylemleri atama olmadan içinde yer alan, ayrıca, bu istekleri ile gider `Content-Type`: `text/plain` üstbilgi. Örneğin, düz bir dosya ile çalışırken, bu HTTP içerik olarak alabilirsiniz `text/plain`:

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

Merhaba bir sonraki eylem, başka bir istek gövdesi hello olarak hello istek göndermesi durumunda (`@body('flatfile')`), hello isteği sahip olabilir bir `text/plain` Content-Type üstbilgisi. Düz metin olan ancak belirtilen üstbilgi olmadığına verilerle çalışıyorsanız, hello veri tootext hello kullanarak el ile çevirebilirsiniz `@string()` işlev, örneğin: `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml ve uygulama/octet-stream ve dönüştürücü işlevleri

Merhaba Logic Apps altyapısı her zaman hello korur `Content-Type` hello HTTP istek veya yanıt alındı. Merhaba altyapısı hello olan içeriği alırsa, bunu `Content-Type` , `application/octet-stream`, ve bir sonraki eylem atama olmadan içeriği, hello giden istek olduğunu dahil `Content-Type`: `application/octet-stream`. Bu şekilde hello altyapısı hello akışı taşırken veri kaybı olmadığından garanti edebilir. Ancak, hello eylem durumu (girişleri ve çıkışları) hello iş akışı durumu ilerler hello gibi bir JSON nesnesinde depolanır. Bu nedenle bazı veri türleri, hello altyapısı dönüştürür toopreserve hello içerik tooa ikili base64 kodlu dize her ikisi de korur uygun meta verilerle `$content` ve `$content-type`, otomatik olarak olduğu dönüştürülmesi. 

* `@json()`-Veri çok çevirir`application/json`
* `@xml()`-Veri çok çevirir`application/xml`
* `@binary()`-Veri çok çevirir`application/octet-stream`
* `@string()`-Veri çok çevirir`text/plain`
* `@base64()`-İçerik tooa base64 dizesi dönüştürür
* `@base64toString()`-base64 ile kodlanmış dize çok dönüştürür`text/plain`
* `@base64toBinary()`-base64 ile kodlanmış dize çok dönüştürür`application/octet-stream`
* `@encodeDataUri()`-dize dataUri bayt dizisi olarak kodlar
* `@decodeDataUri()`-bir dataUri bir bayt dizisine kodunu çözer.

Örneğin, bir HTTP isteğiyle aldıysanız `Content-Type`: `application/xml`:

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

Cast ve daha sonra aşağıdakine benzer ile kullanmak `@xml(triggerBody())`, veya bir işlev `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Diğer içerik türleri

Diğer içerik türleri desteklenir ve logic apps ile çalışır, ancak el ile alınırken hello ileti gövdesi hello çözerek gerektirebilir `$content`. Örneğin, size tetiklemek varsayalım bir `application/x-www-url-formencoded` isteği nereye `$content` olan tüm veri hello yükü kodlanmış bir base64 dizesi toopreserve:

```
CustomerName=Frank&Address=123+Avenue
```

Merhaba isteği düz metin veya JSON olmadığından hello isteği hello eylemde şekilde depolanır:

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Şu anda, form verileri için yerel bir işlevi yoktur, el ile erişerek bu verileri bir iş akışında hala kullanabilirsiniz şekilde hello veri işleviyle ister `@string(body('formdataAction'))`. Giden istek tooalso sahip hello hello istediyseniz `application/x-www-url-formencoded` içerik türü üstbilgisi ekleyebilirsiniz hello isteği toohello eylem gövdesinin gibi herhangi bir atama olmadan `@body('formdataAction')`. Merhaba gövde hello yalnızca hello parametresinde ise ancak, bu yöntem yalnızca çalışır `body` giriş. Toouse çalışırsanız `@body('formdataAction')` içinde bir `application/json` isteği kodlanmış hello gövde gönderdiğinden çalışma zamanı hatası alırsınız.

