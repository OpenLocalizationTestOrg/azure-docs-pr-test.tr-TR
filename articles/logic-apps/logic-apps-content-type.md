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
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="f8c3a-103">Logic apps içinde içerik türlerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="f8c3a-103">Handle content types in logic apps</span></span>

<span data-ttu-id="f8c3a-104">Farklı türlerde içerik JSON, XML, düz dosyalar ve ikili veriler dahil olmak üzere bir mantıksal uygulama akabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="f8c3a-105">Merhaba Logic Apps altyapısı tüm içerik türlerini destekler, ancak bazı yerel hello Logic Apps altyapısı tarafından anlaşılır.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="f8c3a-106">Başkalarının atama veya dönüştürmeler gerektiğinde gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="f8c3a-107">Bu makalede hello altyapısı farklı içerik türlerini nasıl işlediğini ve nasıl toocorrectly ele gerektiğinde bu türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="f8c3a-108">Content-Type üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="f8c3a-108">Content-Type Header</span></span>

<span data-ttu-id="f8c3a-109">toostart temel olarak bakalım iki hello `Content-Types` yok gerektiren dönüştürme veya bir mantıksal uygulama kullanabileceğiniz atama: `application/json` ve `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="f8c3a-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="f8c3a-110">Application/JSON</span></span>

<span data-ttu-id="f8c3a-111">Merhaba iş akışı altyapısı kullanır hello üzerinde `Content-Type` HTTP başlığından toodetermine hello uygun işleme çağırır.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="f8c3a-112">Merhaba içerik türü herhangi bir istekle `application/json` depolanır ve bir JSON nesnesi olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="f8c3a-113">Ayrıca, herhangi bir atama gerek kalmadan JSON içeriği, varsayılan olarak'e ayrıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="f8c3a-114">Örneğin, hello içerik türü üstbilgisi bir istek ayrıştırılamıyor `application/json ` gibi bir ifade kullanarak bir iş akışında `@body('myAction')['foo'][0]` tooget hello değeri `bar` bu durumda:</span><span class="sxs-lookup"><span data-stu-id="f8c3a-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="f8c3a-115">Hiçbir ek atama gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-115">No additional casting is needed.</span></span> <span data-ttu-id="f8c3a-116">JSON ancak belirtilen üstbilgi olmadığına verileri ile çalışıyorsanız, el ile hello kullanarak tooJSON çevirebilirsiniz `@json()` işlev, örneğin: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="f8c3a-117">Şema ve şema Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="f8c3a-117">Schema and schema generator</span></span>

<span data-ttu-id="f8c3a-118">Merhaba isteği tetikleyici tooenter JSON şeması sağlar tooreceive beklediğiniz için hello yükü.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="f8c3a-119">Bu şemayı hello isteği Merhaba içeriğine tüketebileceği şekilde belirteçleri oluşturmak hello designer sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="f8c3a-120">Bir şema hazır yoksa seçin **kullanım örnek yükü toogenerate şeması**, bir örnek yükü JSON şeması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Şema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="f8c3a-122">'Parse JSON' eylemi</span><span class="sxs-lookup"><span data-stu-id="f8c3a-122">'Parse JSON' action</span></span>

<span data-ttu-id="f8c3a-123">Merhaba `Parse JSON` eylem mantığı uygulama tüketimi için kolay belirteçler içine JSON içeriği ayrıştırılamıyor olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="f8c3a-124">Benzer toohello isteği tetikleyici, bu eylem, girin ya da hello tooparse istediğiniz içerik için JSON şeması oluşturma sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="f8c3a-125">Bu araç Süren veri Service Bus, Azure Cosmos DB ve vb. kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![JSON ayrıştırılamıyor](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="f8c3a-127">Metin/düz</span><span class="sxs-lookup"><span data-stu-id="f8c3a-127">Text/plain</span></span>

<span data-ttu-id="f8c3a-128">Benzer çok`application/json`, hello ile alınan HTTP iletisi `Content-Type` üstbilgisinin `text/plain` ham biçiminde depolanır.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="f8c3a-129">Bu ileti sonraki eylemleri atama olmadan içinde yer alan, ayrıca, bu istekleri ile gider `Content-Type`: `text/plain` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="f8c3a-130">Örneğin, düz bir dosya ile çalışırken, bu HTTP içerik olarak alabilirsiniz `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="f8c3a-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="f8c3a-131">Merhaba bir sonraki eylem, başka bir istek gövdesi hello olarak hello istek göndermesi durumunda (`@body('flatfile')`), hello isteği sahip olabilir bir `text/plain` Content-Type üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="f8c3a-132">Düz metin olan ancak belirtilen üstbilgi olmadığına verilerle çalışıyorsanız, hello veri tootext hello kullanarak el ile çevirebilirsiniz `@string()` işlev, örneğin: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="f8c3a-133">Application/xml ve uygulama/octet-stream ve dönüştürücü işlevleri</span><span class="sxs-lookup"><span data-stu-id="f8c3a-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="f8c3a-134">Merhaba Logic Apps altyapısı her zaman hello korur `Content-Type` hello HTTP istek veya yanıt alındı.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="f8c3a-135">Merhaba altyapısı hello olan içeriği alırsa, bunu `Content-Type` , `application/octet-stream`, ve bir sonraki eylem atama olmadan içeriği, hello giden istek olduğunu dahil `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="f8c3a-136">Bu şekilde hello altyapısı hello akışı taşırken veri kaybı olmadığından garanti edebilir.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="f8c3a-137">Ancak, hello eylem durumu (girişleri ve çıkışları) hello iş akışı durumu ilerler hello gibi bir JSON nesnesinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="f8c3a-138">Bu nedenle bazı veri türleri, hello altyapısı dönüştürür toopreserve hello içerik tooa ikili base64 kodlu dize her ikisi de korur uygun meta verilerle `$content` ve `$content-type`, otomatik olarak olduğu dönüştürülmesi.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="f8c3a-139">`@json()`-Veri çok çevirir`application/json`</span><span class="sxs-lookup"><span data-stu-id="f8c3a-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="f8c3a-140">`@xml()`-Veri çok çevirir`application/xml`</span><span class="sxs-lookup"><span data-stu-id="f8c3a-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="f8c3a-141">`@binary()`-Veri çok çevirir`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="f8c3a-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="f8c3a-142">`@string()`-Veri çok çevirir`text/plain`</span><span class="sxs-lookup"><span data-stu-id="f8c3a-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="f8c3a-143">`@base64()`-İçerik tooa base64 dizesi dönüştürür</span><span class="sxs-lookup"><span data-stu-id="f8c3a-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="f8c3a-144">`@base64toString()`-base64 ile kodlanmış dize çok dönüştürür`text/plain`</span><span class="sxs-lookup"><span data-stu-id="f8c3a-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="f8c3a-145">`@base64toBinary()`-base64 ile kodlanmış dize çok dönüştürür`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="f8c3a-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="f8c3a-146">`@encodeDataUri()`-dize dataUri bayt dizisi olarak kodlar</span><span class="sxs-lookup"><span data-stu-id="f8c3a-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="f8c3a-147">`@decodeDataUri()`-bir dataUri bir bayt dizisine kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="f8c3a-148">Örneğin, bir HTTP isteğiyle aldıysanız `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="f8c3a-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="f8c3a-149">Cast ve daha sonra aşağıdakine benzer ile kullanmak `@xml(triggerBody())`, veya bir işlev `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="f8c3a-150">Diğer içerik türleri</span><span class="sxs-lookup"><span data-stu-id="f8c3a-150">Other content types</span></span>

<span data-ttu-id="f8c3a-151">Diğer içerik türleri desteklenir ve logic apps ile çalışır, ancak el ile alınırken hello ileti gövdesi hello çözerek gerektirebilir `$content`.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="f8c3a-152">Örneğin, size tetiklemek varsayalım bir `application/x-www-url-formencoded` isteği nereye `$content` olan tüm veri hello yükü kodlanmış bir base64 dizesi toopreserve:</span><span class="sxs-lookup"><span data-stu-id="f8c3a-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="f8c3a-153">Merhaba isteği düz metin veya JSON olmadığından hello isteği hello eylemde şekilde depolanır:</span><span class="sxs-lookup"><span data-stu-id="f8c3a-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Şu anda, form verileri için yerel bir işlevi yoktur, el ile erişerek bu verileri bir iş akışında hala kullanabilirsiniz şekilde hello veri işleviyle ister `@string(body('formdataAction'))`. Giden istek tooalso sahip hello hello istediyseniz `application/x-www-url-formencoded` içerik türü üstbilgisi ekleyebilirsiniz hello isteği toohello eylem gövdesinin gibi herhangi bir atama olmadan `@body('formdataAction')`. Merhaba gövde hello yalnızca hello parametresinde ise ancak, bu yöntem yalnızca çalışır `body` giriş. <span data-ttu-id="f8c3a-157">Toouse çalışırsanız `@body('formdataAction')` içinde bir `application/json` isteği kodlanmış hello gövde gönderdiğinden çalışma zamanı hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f8c3a-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

