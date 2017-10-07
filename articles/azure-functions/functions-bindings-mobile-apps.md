---
title: "aaaAzure işlevleri Mobile Apps bağlamaları | Microsoft Docs"
description: "Anlamak nasıl toouse Azure Mobile Apps bağlamaları Azure işlevlerinde."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="d7dda-104">Azure işlevleri Mobile Apps bağlamaları</span><span class="sxs-lookup"><span data-stu-id="d7dda-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d7dda-105">Bu makalede açıklanır nasıl tooconfigure ve kod [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) Azure işlevlerinde bağlar.</span><span class="sxs-lookup"><span data-stu-id="d7dda-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="d7dda-106">Giriş ve Mobile Apps için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="d7dda-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="d7dda-107">Merhaba Mobile Apps giriş ve çıkış bağlamaları izin [okuma ve yazma toodata tabloları](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) mobil uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="d7dda-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="d7dda-108">Mobile Apps giriş bağlama</span><span class="sxs-lookup"><span data-stu-id="d7dda-108">Mobile Apps input binding</span></span>
<span data-ttu-id="d7dda-109">Merhaba Mobile Apps giriş bağlaması bir kaydı bir mobil tablo uç noktasından yükler ve işlevinizin geçirir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="d7dda-110">C# ve F # işlevleri herhangi bir yapılan değişiklikler toohello kaydı otomatik olarak gönderilir geri toohello tablo hello işlevi başarıyla çıktığında.</span><span class="sxs-lookup"><span data-stu-id="d7dda-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="d7dda-111">Merhaba Mobile Apps giriş tooa işlevini kullanan hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d7dda-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="d7dda-112">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d7dda-112">Note hello following:</span></span>

* <span data-ttu-id="d7dda-113">`id`Merhaba işlevi çağırır hello Tetikle dayanabilir veya statik olabilir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="d7dda-114">Kullanırsanız, örneğin, bir [sıra tetikleyici]() , işlev, ardından `"id": "{queueTrigger}"` kullandığı hello hello kuyruk iletisini dize değerini kayıt kimliği tooretrieve hello gibi.</span><span class="sxs-lookup"><span data-stu-id="d7dda-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="d7dda-115">`connection`bir uygulama ayarı sırayla mobil uygulamanızı hello URL'sini içeren işlevi uygulamanızda Hello adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="d7dda-116">Bu URL tooconstruct gerekli hello REST işlemlerini mobil uygulamanızı karşı Hello işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d7dda-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="d7dda-117">[İşlevi uygulamanıza bir uygulama ayarı oluşturmak]() , mobil uygulamanızın URL'si içeren (gibi görünen `http://<appname>.azurewebsites.net`), ardından hello hello uygulama ayarı hello adını belirtin `connection` giriş bağlaması özelliği.</span><span class="sxs-lookup"><span data-stu-id="d7dda-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="d7dda-118">Toospecify gerek `apiKey` varsa, [bir API anahtarı, Node.js mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), veya [bir API anahtarı, .NET Mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="d7dda-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="d7dda-119">toodo bunu, [işlevi uygulamanıza bir uygulama ayarı oluşturmak]() hello API anahtarı içeren, hello eklemek `apiKey` giriş bağlamanız hello uygulama ayarı hello adıyla bir özellik.</span><span class="sxs-lookup"><span data-stu-id="d7dda-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="d7dda-120">Bu API anahtarı ile mobil uygulama istemcilerinizi paylaşılmayan gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="d7dda-121">Yalnızca Azure işlevleri gibi dağıtılmış güvenli bir şekilde tooservice tarafı istemcileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="d7dda-122">Azure işlevleri depolar bağlantı bilgilerini ve API anahtarlarını uygulama ayarlarda böylece kaynak denetimi deponuzun denetlenmez.</span><span class="sxs-lookup"><span data-stu-id="d7dda-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="d7dda-123">Bu, hassas bilgilerinizi koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7dda-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="d7dda-124">Giriş kullanımı</span><span class="sxs-lookup"><span data-stu-id="d7dda-124">Input usage</span></span>
<span data-ttu-id="d7dda-125">Bu bölümde, işlev kodunuzda bağlama toouse mobil uygulamalarınızı nasıl giriş gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="d7dda-126">Merhaba Hello kaydıyla tablo ve kayıt kimliği bulundu belirtildiğinde adlı hello geçirilir [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parametresi (veya Node.js içinde hello geçirilir `context.bindings.<name>` nesnesi).</span><span class="sxs-lookup"><span data-stu-id="d7dda-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="d7dda-127">Merhaba kayıt bulunamadı, hello parametredir `null`.</span><span class="sxs-lookup"><span data-stu-id="d7dda-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="d7dda-128">C# ve F # işlevleri giriş toohello kaydı (giriş parametresi) yaptığınız tüm değişiklikler otomatik olarak gönderilen geri toohello Mobile Apps tablo hello işlevi başarıyla çıktığında.</span><span class="sxs-lookup"><span data-stu-id="d7dda-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="d7dda-129">Node.js işlevlerini kullanmak `context.bindings.<name>` tooaccess hello Giriş kaydı.</span><span class="sxs-lookup"><span data-stu-id="d7dda-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="d7dda-130">Node.js kaydında değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7dda-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="d7dda-131">Giriş örneği</span><span class="sxs-lookup"><span data-stu-id="d7dda-131">Input sample</span></span>
<span data-ttu-id="d7dda-132">Function.json aşağıdaki hello olduğunu varsayalım, bir mobil uygulama tablosu kaydı hello kuyruk tetikleyici iletisi hello kimliği alır:</span><span class="sxs-lookup"><span data-stu-id="d7dda-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="d7dda-133">Merhaba bağlama girdi kaydından hello kullanan hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="d7dda-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="d7dda-134">Merhaba C# ve F # örnekleri ayrıca hello kaydın değişiklik `text` özelliği.</span><span class="sxs-lookup"><span data-stu-id="d7dda-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="d7dda-135">C#</span><span class="sxs-lookup"><span data-stu-id="d7dda-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="d7dda-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="d7dda-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="d7dda-137">C# giriş örneği</span><span class="sxs-lookup"><span data-stu-id="d7dda-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="d7dda-138">Node.js giriş örneği</span><span class="sxs-lookup"><span data-stu-id="d7dda-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="d7dda-139">Mobile Apps bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="d7dda-139">Mobile Apps output binding</span></span>
<span data-ttu-id="d7dda-140">Merhaba Mobile Apps çıkış bağlama toowrite yeni bir kayıt tooa Mobile Apps tablo uç noktası kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7dda-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="d7dda-141">Merhaba Mobile Apps hello JSON nesnesinde aşağıdaki hello işlevi kullanan çıktısı `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d7dda-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="d7dda-142">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d7dda-142">Note hello following:</span></span>

* <span data-ttu-id="d7dda-143">`connection`bir uygulama ayarı sırayla mobil uygulamanızı hello URL'sini içeren işlevi uygulamanızda Hello adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="d7dda-144">Bu URL tooconstruct gerekli hello REST işlemlerini mobil uygulamanızı karşı Hello işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d7dda-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="d7dda-145">[İşlevi uygulamanıza bir uygulama ayarı oluşturmak]() , mobil uygulamanızın URL'si içeren (gibi görünen `http://<appname>.azurewebsites.net`), ardından hello hello uygulama ayarı hello adını belirtin `connection` giriş bağlaması özelliği.</span><span class="sxs-lookup"><span data-stu-id="d7dda-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="d7dda-146">Toospecify gerek `apiKey` varsa, [bir API anahtarı, Node.js mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), veya [bir API anahtarı, .NET Mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="d7dda-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="d7dda-147">toodo bunu, [işlevi uygulamanıza bir uygulama ayarı oluşturmak]() hello API anahtarı içeren, hello eklemek `apiKey` giriş bağlamanız hello uygulama ayarı hello adıyla bir özellik.</span><span class="sxs-lookup"><span data-stu-id="d7dda-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="d7dda-148">Bu API anahtarı ile mobil uygulama istemcilerinizi paylaşılmayan gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="d7dda-149">Yalnızca Azure işlevleri gibi dağıtılmış güvenli bir şekilde tooservice tarafı istemcileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="d7dda-150">Azure işlevleri depolar bağlantı bilgilerini ve API anahtarlarını uygulama ayarlarda böylece kaynak denetimi deponuzun denetlenmez.</span><span class="sxs-lookup"><span data-stu-id="d7dda-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="d7dda-151">Bu, hassas bilgilerinizi koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7dda-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="d7dda-152">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="d7dda-152">Output usage</span></span>
<span data-ttu-id="d7dda-153">Bu bölümde işlevi kodunuzda bağlama toouse mobil uygulamalarınızı nasıl çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7dda-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="d7dda-154">C# işlevlerde, türünde bir adlandırılmış çıktı parametresi kullanın `out object` tooaccess hello çıkış kaydı.</span><span class="sxs-lookup"><span data-stu-id="d7dda-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="d7dda-155">Node.js işlevlerini kullanmak `context.bindings.<name>` tooaccess hello çıkış kaydı.</span><span class="sxs-lookup"><span data-stu-id="d7dda-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="d7dda-156">Çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="d7dda-156">Output sample</span></span>
<span data-ttu-id="d7dda-157">Bir kuyruk tetikleyici ve Mobile Apps çıkış tanımlayan function.json aşağıdaki hello olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d7dda-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="d7dda-158">Merhaba Mobile Apps tablo endpoint hello kuyruk iletisi Merhaba içeriğine sahip bir kayıt oluşturur hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="d7dda-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="d7dda-159">C#</span><span class="sxs-lookup"><span data-stu-id="d7dda-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="d7dda-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="d7dda-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="d7dda-161">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="d7dda-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="d7dda-162">Node.js çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="d7dda-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="d7dda-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7dda-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

