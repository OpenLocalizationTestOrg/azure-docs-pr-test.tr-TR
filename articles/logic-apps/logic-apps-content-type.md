---
title: "İçerik türleri - Azure mantıksal uygulamaları işlemek | Microsoft Docs"
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
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="abd6a-103">Logic apps içinde içerik türlerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="abd6a-103">Handle content types in logic apps</span></span>

<span data-ttu-id="abd6a-104">Farklı türlerde içerik JSON, XML, düz dosyalar ve ikili veriler dahil olmak üzere bir mantıksal uygulama akabilir.</span><span class="sxs-lookup"><span data-stu-id="abd6a-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="abd6a-105">Logic Apps altyapısı tüm içerik türlerini destekler, ancak bazı yerel Logic Apps altyapısı tarafından anlaşılır.</span><span class="sxs-lookup"><span data-stu-id="abd6a-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="abd6a-106">Başkalarının atama veya dönüştürmeler gerektiğinde gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="abd6a-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="abd6a-107">Bu makalede altyapısı farklı içerik türlerini nasıl işlediğini ve doğru bir şekilde gerektiğinde bu türleri nasıl ele alınacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="abd6a-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="abd6a-108">Content-Type üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="abd6a-108">Content-Type Header</span></span>

<span data-ttu-id="abd6a-109">Temel olarak başlatmak için iki bakalım `Content-Types` yok gerektiren dönüştürme veya bir mantıksal uygulama kullanabileceğiniz atama: `application/json` ve `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="abd6a-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="abd6a-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="abd6a-110">Application/JSON</span></span>

<span data-ttu-id="abd6a-111">İş akışı altyapısının dayanan `Content-Type` uygun işleme belirlemek için HTTP başlığından çağırır.</span><span class="sxs-lookup"><span data-stu-id="abd6a-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="abd6a-112">İçerik türü herhangi bir istekle `application/json` depolanır ve bir JSON nesnesi olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="abd6a-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="abd6a-113">Ayrıca, herhangi bir atama gerek kalmadan JSON içeriği, varsayılan olarak'e ayrıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="abd6a-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="abd6a-114">Örneğin, içerik türü üstbilgisi bir istek ayrıştırılamıyor `application/json ` gibi bir ifade kullanarak bir iş akışında `@body('myAction')['foo'][0]` değeri almaya `bar` bu durumda:</span><span class="sxs-lookup"><span data-stu-id="abd6a-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="abd6a-115">Hiçbir ek atama gereklidir.</span><span class="sxs-lookup"><span data-stu-id="abd6a-115">No additional casting is needed.</span></span> <span data-ttu-id="abd6a-116">JSON ancak belirtilen üstbilgi olmadığına verileri ile çalışıyorsanız, el ile JSON kullanmaya çevirebilirsiniz `@json()` işlev, örneğin: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="abd6a-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="abd6a-117">Şema ve şema Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="abd6a-117">Schema and schema generator</span></span>

<span data-ttu-id="abd6a-118">İstek tetikleyici için almayı beklediğiniz yükü JSON şeması girmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="abd6a-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="abd6a-119">İstek içeriği tüketebileceği şekilde bu şema Tasarımcısı generate belirteçleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="abd6a-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="abd6a-120">Bir şema hazır yoksa seçin **şema üretmek için kullanım örnek yük**, bir örnek yükü JSON şeması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abd6a-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Şema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="abd6a-122">'Parse JSON' eylemi</span><span class="sxs-lookup"><span data-stu-id="abd6a-122">'Parse JSON' action</span></span>

<span data-ttu-id="abd6a-123">`Parse JSON` Eylem mantığı uygulama tüketimi için kolay belirteçler içine JSON içeriği ayrıştırılamıyor olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="abd6a-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="abd6a-124">Benzer şekilde istek tetikleyici, bu eylem girin veya ayrıştırma istediğiniz içerik için JSON şeması oluşturma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="abd6a-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="abd6a-125">Bu araç Süren veri Service Bus, Azure Cosmos DB ve vb. kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="abd6a-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![JSON ayrıştırılamıyor](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="abd6a-127">Metin/düz</span><span class="sxs-lookup"><span data-stu-id="abd6a-127">Text/plain</span></span>

<span data-ttu-id="abd6a-128">Benzer şekilde `application/json`, HTTP iletileri ile alınan `Content-Type` üstbilgisinin `text/plain` ham biçiminde depolanır.</span><span class="sxs-lookup"><span data-stu-id="abd6a-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="abd6a-129">Bu ileti sonraki eylemleri atama olmadan içinde yer alan, ayrıca, bu istekleri ile gider `Content-Type`: `text/plain` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="abd6a-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="abd6a-130">Örneğin, düz bir dosya ile çalışırken, bu HTTP içerik olarak alabilirsiniz `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="abd6a-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="abd6a-131">Bir sonraki eylem, başka bir istek gövdesi olarak istek göndermesi durumunda (`@body('flatfile')`), istek olması gereken bir `text/plain` Content-Type üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="abd6a-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="abd6a-132">Düz metin olan ancak belirtilen üstbilgi olmadığına verilerle çalışıyorsanız, metin kullanarak verileri el ile çevirebilirsiniz `@string()` işlev, örneğin: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="abd6a-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="abd6a-133">Application/xml ve uygulama/octet-stream ve dönüştürücü işlevleri</span><span class="sxs-lookup"><span data-stu-id="abd6a-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="abd6a-134">Logic Apps altyapısı her zaman korur `Content-Type` HTTP isteği veya yanıtı alınmadı.</span><span class="sxs-lookup"><span data-stu-id="abd6a-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="abd6a-135">Altyapı olan içeriği alırsa, bunu `Content-Type` , `application/octet-stream`, ve bir sonraki eylem atama olmadan içeriği, giden istek olduğunu dahil `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="abd6a-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="abd6a-136">Bu şekilde, iş akışı taşırken veri kaybı olmadığından altyapısı garanti edebilir.</span><span class="sxs-lookup"><span data-stu-id="abd6a-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="abd6a-137">Ancak, iş akışı durumu hareket ederken eylem durumu (girişleri ve çıkışları) bir JSON nesnesinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="abd6a-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="abd6a-138">Bazı veri türleri korumak için her ikisi de korur uygun meta verilerle ikili base64 ile kodlanmış dizeye içerik altyapısı dönüştürür şekilde `$content` ve `$content-type`, otomatik olarak olduğu dönüştürülmesi.</span><span class="sxs-lookup"><span data-stu-id="abd6a-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="abd6a-139">`@json()`-Veri çevirir`application/json`</span><span class="sxs-lookup"><span data-stu-id="abd6a-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="abd6a-140">`@xml()`-Veri çevirir`application/xml`</span><span class="sxs-lookup"><span data-stu-id="abd6a-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="abd6a-141">`@binary()`-Veri çevirir`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="abd6a-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="abd6a-142">`@string()`-Veri çevirir`text/plain`</span><span class="sxs-lookup"><span data-stu-id="abd6a-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="abd6a-143">`@base64()`-İçerik base64 dizeye dönüştürür</span><span class="sxs-lookup"><span data-stu-id="abd6a-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="abd6a-144">`@base64toString()`-base64 ile kodlanmış dizeye dönüştürür`text/plain`</span><span class="sxs-lookup"><span data-stu-id="abd6a-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="abd6a-145">`@base64toBinary()`-base64 ile kodlanmış dizeye dönüştürür`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="abd6a-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="abd6a-146">`@encodeDataUri()`-dize dataUri bayt dizisi olarak kodlar</span><span class="sxs-lookup"><span data-stu-id="abd6a-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="abd6a-147">`@decodeDataUri()`-bir dataUri bir bayt dizisine kodunu çözer.</span><span class="sxs-lookup"><span data-stu-id="abd6a-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="abd6a-148">Örneğin, bir HTTP isteğiyle aldıysanız `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="abd6a-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="abd6a-149">Cast ve daha sonra aşağıdakine benzer ile kullanmak `@xml(triggerBody())`, veya bir işlev `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="abd6a-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="abd6a-150">Diğer içerik türleri</span><span class="sxs-lookup"><span data-stu-id="abd6a-150">Other content types</span></span>

<span data-ttu-id="abd6a-151">Diğer içerik türleri desteklenir ve logic apps ile çalışır, ancak ileti gövdesi çözerek el ile alma gerektirebilir `$content`.</span><span class="sxs-lookup"><span data-stu-id="abd6a-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="abd6a-152">Örneğin, size tetiklemek varsayalım bir `application/x-www-url-formencoded` isteği nereye `$content` olan tüm verileri korumak için bir base64 dizesi kodlanmış yükü:</span><span class="sxs-lookup"><span data-stu-id="abd6a-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="abd6a-153">Düz metin veya JSON isteği olmadığı için istek eyleminde şekilde depolanır:</span><span class="sxs-lookup"><span data-stu-id="abd6a-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Şu anda, form verileri için yerel bir işlevi yoktur, bir işlev verilerle el ile erişerek bu verileri bir iş akışında hala kullanabilirsiniz şekilde ister `@string(body('formdataAction'))`. Ayrıca yönelik giden istek istediyseniz `application/x-www-url-formencoded` içerik türü üstbilgisi ekleyebilirsiniz istek eylem gövdeye gibi herhangi bir atama olmadan `@body('formdataAction')`. Gövde yalnızca parametresinde ise ancak, bu yöntem yalnızca çalışır `body` giriş. <span data-ttu-id="abd6a-157">Kullanmayı denerseniz `@body('formdataAction')` içinde bir `application/json` isteği kodlu gövde gönderdiğinden çalışma zamanı hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="abd6a-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

