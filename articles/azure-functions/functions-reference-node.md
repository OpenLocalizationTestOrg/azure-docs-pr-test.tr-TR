---
title: "Azure işlevleri için aaaJavaScript Geliştirici Başvurusu | Microsoft Docs"
description: "JavaScript kullanarak toodevelop nasıl çalıştığını anlayın."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="4abda-104">Azure işlevleri JavaScript Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="4abda-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4abda-105">C# betiği</span><span class="sxs-lookup"><span data-stu-id="4abda-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="4abda-106">F # betiği</span><span class="sxs-lookup"><span data-stu-id="4abda-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="4abda-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="4abda-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="4abda-108">Azure işlevleri kolaylaştırır kolay tooexport olarak geçirilen bir işlev için JavaScript deneyimi hello bir `context` alırken ve verileri bağlamaları aracılığıyla gönderme ve hello çalışma zamanı ile iletişim kurmak için nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="4abda-109">Bu makalede, zaten hello okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="4abda-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="4abda-110">Bir işlev dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="4abda-110">Exporting a function</span></span>
<span data-ttu-id="4abda-111">Tüm JavaScript işlevleri tek bir dışarı aktarma `function` aracılığıyla `module.exports` hello çalışma zamanı için toofind hello işlevi ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4abda-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="4abda-112">Bu işlev, her zaman içermelidir bir `context` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4abda-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="4abda-113">Bağlamaları `direction === "in"` boyunca kullanabileceğiniz anlamına gelir işlevi bağımsız geçirilen [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically işlemek yeni girişleri (kullanarak örneğin, `arguments.length` tooiterate tüm girişlerinizi üzerinden).</span><span class="sxs-lookup"><span data-stu-id="4abda-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="4abda-114">Yalnızca bir tetikleyici ve hiçbir ek girişleri varsa başvurulmadan beklendiği tetikleyici verilerinize erişebilir bu işlevi kullanışlı çünkü, `context` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4abda-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="4abda-115">Merhaba bağımsız değişkenleri toohello işlevi içinde gerçekleşme içinde hello sırayla boyunca her zaman geçirilir *function.json*dışarı deyiminizde belirtmeyin olsa bile.</span><span class="sxs-lookup"><span data-stu-id="4abda-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="4abda-116">Örneğin, `function(context, a, b)` ve çok değiştirme`function(context, a)`, hello değerini almaya devam `b` çok başvuran tarafından işlevi kodda`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="4abda-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="4abda-117">Yönü, bağımsız olarak tüm bağlamaları ayrıca boyunca üzerinde hello geçirilen `context` (komut dosyası izleyen hello bakın) nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="4abda-118">bağlam nesnesi</span><span class="sxs-lookup"><span data-stu-id="4abda-118">context object</span></span>
<span data-ttu-id="4abda-119">Merhaba çalışma zamanı modülünü kullanan bir `context` nesne toopass veri tooand işlevi ve toolet hello çalışma zamanı ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="4abda-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="4abda-120">Merhaba bağlam nesnesi her zaman hello ilk parametre tooa işlev ve yöntemleri gibi içerdiğinden dahil edilmelidir `context.done` ve `context.log`, olan gerekli toouse hello çalışma zamanı doğru.</span><span class="sxs-lookup"><span data-stu-id="4abda-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="4abda-121">Ne olursa olsun ister misiniz hello nesne adı verebilirsiniz (örneğin, `ctx` veya `c`).</span><span class="sxs-lookup"><span data-stu-id="4abda-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="4abda-122">Context.Bindings özelliği</span><span class="sxs-lookup"><span data-stu-id="4abda-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="4abda-123">Tüm girdi ve çıktı verilerini içeren adlandırılmış bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="4abda-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="4abda-124">Örneğin, bağlama tanımı'nda aşağıdaki Merhaba, *function.json* size erişim sağlar hello hello hello sıradan içeriğini `context.bindings.myInput` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4abda-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="4abda-125">Context.Done yöntemi</span><span class="sxs-lookup"><span data-stu-id="4abda-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="4abda-126">Kodunuzu bitirdi hello çalışma zamanı bildirir.</span><span class="sxs-lookup"><span data-stu-id="4abda-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="4abda-127">Çağırmalısınız `context.done`, veya başka hello çalışma zamanı hiçbir zaman bilir işlevinizi tamamlandıktan ve hello yürütme zaman aşımı olur.</span><span class="sxs-lookup"><span data-stu-id="4abda-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="4abda-128">Merhaba `context.done` yöntemi sağlar, toopass başa bir kullanıcı tanımlı hata toohello çalışma zamanı ve bir özellik paketi hello hello özellikleri üzerine özelliklerinin `context.bindings` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4abda-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="4abda-129">Context.log yöntemi</span><span class="sxs-lookup"><span data-stu-id="4abda-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="4abda-130">Toowrite toohello akış konsol günlükleri hello varsayılan izleme düzeyinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="4abda-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="4abda-131">Üzerinde `context.log`, ek yöntemleri günlüğü toohello konsol günlüğüne diğer izleme düzeyleri yazmanıza olanak tanıyan kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="4abda-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="4abda-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4abda-132">Method</span></span>                 | <span data-ttu-id="4abda-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4abda-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="4abda-134">**hata (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="4abda-134">**error(_message_)**</span></span>   | <span data-ttu-id="4abda-135">Oturum açma veya alt tooerror düzeyinde yazar.</span><span class="sxs-lookup"><span data-stu-id="4abda-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="4abda-136">**warn (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="4abda-136">**warn(_message_)**</span></span>    | <span data-ttu-id="4abda-137">Oturum açma veya alt toowarning düzeyinde yazar.</span><span class="sxs-lookup"><span data-stu-id="4abda-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="4abda-138">**bilgi (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="4abda-138">**info(_message_)**</span></span>    | <span data-ttu-id="4abda-139">Oturum açma veya alt tooinfo düzeyinde yazar.</span><span class="sxs-lookup"><span data-stu-id="4abda-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="4abda-140">**verbose (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="4abda-140">**verbose(_message_)**</span></span> | <span data-ttu-id="4abda-141">Tooverbose düzeyinde günlüğe kaydetme yazar.</span><span class="sxs-lookup"><span data-stu-id="4abda-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="4abda-142">Merhaba aşağıdaki örnek hello uyarı izleme düzeyi toohello konsolda Yazar:</span><span class="sxs-lookup"><span data-stu-id="4abda-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="4abda-143">Merhaba host.json dosyasında günlüğe kaydetme için hello izleme düzeyi eşiğini ayarlayın ya da kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4abda-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="4abda-144">Nasıl toowrite toohello günlükleri hakkında daha fazla bilgi için hello sonraki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="4abda-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="4abda-145">Bağlama veri türü</span><span class="sxs-lookup"><span data-stu-id="4abda-145">Binding data type</span></span>

<span data-ttu-id="4abda-146">toodefine hello kullanmak için bir giriş bağlama, hello veri türü `dataType` hello bağlama tanımında özelliği.</span><span class="sxs-lookup"><span data-stu-id="4abda-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="4abda-147">Örneğin, tooread ikili biçimde bir HTTP isteğinin içerik Merhaba, hello türünü kullanmak `binary`:</span><span class="sxs-lookup"><span data-stu-id="4abda-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="4abda-148">Diğer seçenekler için `dataType` olan `stream` ve `string`.</span><span class="sxs-lookup"><span data-stu-id="4abda-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="4abda-149">Yazma İzleme çıktısı toohello konsol</span><span class="sxs-lookup"><span data-stu-id="4abda-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="4abda-150">İşlevlerde, kullandığınız hello `context.log` yöntemleri toowrite İzleme çıktısı toohello konsol.</span><span class="sxs-lookup"><span data-stu-id="4abda-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="4abda-151">Bu noktada, kullanamazsınız `console.log` toowrite toohello konsol.</span><span class="sxs-lookup"><span data-stu-id="4abda-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="4abda-152">Çağırdığınızda `context.log()`, iletinizi hello olduğu hello varsayılan izleme düzeyi toohello konsolda yazılır _bilgisi_ izleme düzeyi.</span><span class="sxs-lookup"><span data-stu-id="4abda-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="4abda-153">Merhaba aşağıdaki kod hello bilgi izleme düzeyini toohello konsolda Yazar:</span><span class="sxs-lookup"><span data-stu-id="4abda-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="4abda-154">Hello önceki kod eşdeğer toohello kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4abda-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="4abda-155">Merhaba aşağıdaki kod toohello konsol hello hata düzeyinde Yazar:</span><span class="sxs-lookup"><span data-stu-id="4abda-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="4abda-156">Çünkü _hata_ hello yüksek izleme günlüğü etkin olduğu sürece düzeyi, bu izleme toohello çıktısı tüm izleme düzeylerde yazılır.</span><span class="sxs-lookup"><span data-stu-id="4abda-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="4abda-157">Tüm `context.log` yöntemlerini desteklemek hello Node.js hello tarafından desteklenen aynı parametre biçimi [util.format yöntemi](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="4abda-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="4abda-158">Merhaba varsayılan izleme düzeyi kullanarak toohello konsol yazar kod aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4abda-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="4abda-159">Ayrıca, aynı hello biçimini izleyen kod yazma hello de yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4abda-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="4abda-160">Konsol günlüğe kaydetme için Hello izleme düzeyini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4abda-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="4abda-161">İşlevler izlemeleri, işlevlerden toohello konsol yazılır kolay toocontrol hello şekilde kolaylaştırır toohello konsol yazma hello eşik izleme düzeyi tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4abda-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="4abda-162">tooset hello eşik toohello konsol, kullanım hello yazılan tüm izlemeleri için `tracing.consoleLevel` hello host.json dosyasında özellik.</span><span class="sxs-lookup"><span data-stu-id="4abda-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="4abda-163">Bu ayar işlevi uygulamanızı tooall işlevlerinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4abda-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="4abda-164">Merhaba aşağıdaki örnek hello izleme eşik tooenable ayrıntılı günlük kaydını ayarlar:</span><span class="sxs-lookup"><span data-stu-id="4abda-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="4abda-165">Değerleri **consoleLevel** hello toohello adlarını karşılık `context.log` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="4abda-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="4abda-166">Tüm izleme toohello konsol oturum toodisable ayarlamak **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="4abda-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="4abda-167">Merhaba hello host.json dosyası hakkında daha fazla bilgi için bkz: [host.json başvuru konusu](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="4abda-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="4abda-168">HTTP Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="4abda-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="4abda-169">HTTP ve Web kancası Tetikleyicileri ve bağlamaları istek ve yanıt nesneleri toorepresent hello HTTP Mesajlaşma kullanmak çıktı.</span><span class="sxs-lookup"><span data-stu-id="4abda-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="4abda-170">İstek nesnesi</span><span class="sxs-lookup"><span data-stu-id="4abda-170">Request object</span></span>

<span data-ttu-id="4abda-171">Merhaba `request` nesnesi hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4abda-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="4abda-172">Özellik</span><span class="sxs-lookup"><span data-stu-id="4abda-172">Property</span></span>      | <span data-ttu-id="4abda-173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4abda-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="4abda-174">_Gövde_</span><span class="sxs-lookup"><span data-stu-id="4abda-174">_body_</span></span>        | <span data-ttu-id="4abda-175">Merhaba hello istek gövdesini içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="4abda-176">_üstbilgileri_</span><span class="sxs-lookup"><span data-stu-id="4abda-176">_headers_</span></span>     | <span data-ttu-id="4abda-177">Merhaba istek üstbilgileri içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="4abda-178">_yöntemi_</span><span class="sxs-lookup"><span data-stu-id="4abda-178">_method_</span></span>      | <span data-ttu-id="4abda-179">Merhaba hello isteğinin HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4abda-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="4abda-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="4abda-180">_originalUrl_</span></span> | <span data-ttu-id="4abda-181">Merhaba isteği Hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="4abda-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="4abda-182">_parametreleri_</span><span class="sxs-lookup"><span data-stu-id="4abda-182">_params_</span></span>      | <span data-ttu-id="4abda-183">Merhaba isteğinin hello Yönlendirme parametreleri içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="4abda-184">_Sorgu_</span><span class="sxs-lookup"><span data-stu-id="4abda-184">_query_</span></span>       | <span data-ttu-id="4abda-185">Merhaba sorgu parametreleri içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="4abda-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="4abda-186">_rawBody_</span></span>     | <span data-ttu-id="4abda-187">dize olarak hello ileti gövdesi Hello.</span><span class="sxs-lookup"><span data-stu-id="4abda-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="4abda-188">Yanıt nesnesi</span><span class="sxs-lookup"><span data-stu-id="4abda-188">Response object</span></span>

<span data-ttu-id="4abda-189">Merhaba `response` nesnesi hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4abda-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="4abda-190">Özellik</span><span class="sxs-lookup"><span data-stu-id="4abda-190">Property</span></span>  | <span data-ttu-id="4abda-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4abda-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="4abda-192">_Gövde_</span><span class="sxs-lookup"><span data-stu-id="4abda-192">_body_</span></span>    | <span data-ttu-id="4abda-193">Merhaba hello yanıtın gövdesini içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="4abda-194">_üstbilgileri_</span><span class="sxs-lookup"><span data-stu-id="4abda-194">_headers_</span></span> | <span data-ttu-id="4abda-195">Merhaba yanıt üst bilgileri içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="4abda-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="4abda-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="4abda-196">_isRaw_</span></span>   | <span data-ttu-id="4abda-197">Biçimlendirme için hello yanıt atlanır gösterir.</span><span class="sxs-lookup"><span data-stu-id="4abda-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="4abda-198">_durumu_</span><span class="sxs-lookup"><span data-stu-id="4abda-198">_status_</span></span>  | <span data-ttu-id="4abda-199">Merhaba hello yanıtının HTTP durum kodu.</span><span class="sxs-lookup"><span data-stu-id="4abda-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="4abda-200">Merhaba istek ve yanıt erişme</span><span class="sxs-lookup"><span data-stu-id="4abda-200">Accessing hello request and response</span></span> 

<span data-ttu-id="4abda-201">HTTP tetikleyicileri ile çalışırken, herhangi bir üç şekilde hello HTTP istek ve yanıt nesneleri erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4abda-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="4abda-202">Giriş Hello adlı ve bağlamaları çıktı.</span><span class="sxs-lookup"><span data-stu-id="4abda-202">From hello named input and output bindings.</span></span> <span data-ttu-id="4abda-203">Bu şekilde, hello HTTP tetikleyici ve bağlamaları iş aynı herhangi bir bağlama olarak hello.</span><span class="sxs-lookup"><span data-stu-id="4abda-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="4abda-204">Merhaba aşağıdaki örnek hello yanıt nesnesi bir adlandırılmış kullanarak ayarlar `response` bağlama:</span><span class="sxs-lookup"><span data-stu-id="4abda-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="4abda-205">Gelen `req` ve `res` hello özellikleri `context` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4abda-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="4abda-206">Bu şekilde, toouse hello tam sahip olmak yerine hello geleneksel düzeni tooaccess HTTP hello bağlam nesnesi, verilerden kullanabilirsiniz `context.bindings.name` düzeni.</span><span class="sxs-lookup"><span data-stu-id="4abda-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="4abda-207">örnekte gösterildiği nasıl aşağıdaki hello tooaccess hello `req` ve `res` hello nesnelerde `context`:</span><span class="sxs-lookup"><span data-stu-id="4abda-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="4abda-208">Çağırarak `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="4abda-208">By calling `context.done()`.</span></span> <span data-ttu-id="4abda-209">Özel türde bir HTTP bağlaması toohello geçirilen hello yanıtı döndürür `context.done()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4abda-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="4abda-210">HTTP aşağıdaki hello çıktı bağlama tanımlayan bir `$return` çıkış parametresi:</span><span class="sxs-lookup"><span data-stu-id="4abda-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="4abda-211">Bu çıktı bağlama çağırdığınızda toosupply hello yanıt bekliyor `done()`aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4abda-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="4abda-212">Düğüm sürümü ve paket Yönetimi</span><span class="sxs-lookup"><span data-stu-id="4abda-212">Node version and Package Management</span></span>
<span data-ttu-id="4abda-213">Merhaba düğümü sürüm şu anda kilitli `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="4abda-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="4abda-214">Geçerli daha fazla sürümleri için destek eklenmesi araştırma, yapılandırılabilir hale getirme.</span><span class="sxs-lookup"><span data-stu-id="4abda-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="4abda-215">Aşağıdaki adımları hello işlevi uygulamanızda paketleri dahil sağlar:</span><span class="sxs-lookup"><span data-stu-id="4abda-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="4abda-216">Çok Git`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="4abda-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="4abda-217">Tıklatın **Debug konsol** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="4abda-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="4abda-218">Çok Git`D:\home\site\wwwroot`, package.json dosyası toohello sürükleyin **wwwroot** hello sayfasının üst yarı hello klasörü.</span><span class="sxs-lookup"><span data-stu-id="4abda-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="4abda-219">Dosyaları tooyour işlev uygulaması başka yöntemler de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4abda-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="4abda-220">Daha fazla bilgi için bkz: [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="4abda-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="4abda-221">Merhaba package.json dosyası karşıya yüklendikten sonra hello çalıştırmak `npm install` hello komutunu **Kudu uzaktan yürütme konsol**.</span><span class="sxs-lookup"><span data-stu-id="4abda-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="4abda-222">Bu eylem hello package.json dosyasında belirtildiği hello paketleri indirir ve hello işlev uygulaması yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="4abda-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="4abda-223">Merhaba ihtiyacınız paketleri yüklendikten sonra bunları tooyour işlevi çağırarak aldığınız `require('packagename')`, aşağıdaki örneğine hello olarak:</span><span class="sxs-lookup"><span data-stu-id="4abda-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="4abda-224">Tanımlamanız gerekir bir `package.json` dosya işlevi uygulamanızın hello kökü.</span><span class="sxs-lookup"><span data-stu-id="4abda-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="4abda-225">Tanımlama hello dosya aynı önbelleğe alınan paketler hello en iyi performans sağlayan hello hello uygulama paylaşım uygulamasında tüm işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="4abda-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="4abda-226">Sürüm çakışması ortaya çıkarsa, ekleyerek çözebilmek bir `package.json` belirli bir işlev hello klasöründe bulunan dosyadır.</span><span class="sxs-lookup"><span data-stu-id="4abda-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="4abda-227">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="4abda-227">Environment variables</span></span>
<span data-ttu-id="4abda-228">tooget bir ortam değişkeni veya kullanan bir uygulama ayarı değeri `process.env`, aşağıdaki kod örneğine hello gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="4abda-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="4abda-229">JavaScript işlevleri için ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="4abda-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="4abda-230">JavaScript işlevleri ile çalışırken, iki bölüme aşağıdaki hello hello konuları farkında olması.</span><span class="sxs-lookup"><span data-stu-id="4abda-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="4abda-231">Tek çekirdekli uygulama hizmeti planları seçin</span><span class="sxs-lookup"><span data-stu-id="4abda-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="4abda-232">Merhaba uygulama hizmeti planı kullanan bir işlev uygulaması oluşturduğunuzda, bir plan ile birden çok çekirdek yerine bir tek çekirdek planı seçmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="4abda-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="4abda-233">Bugün, işlevleri çalışır JavaScript işlevleri daha verimli bir şekilde tek çekirdekli sanal makineler ve büyük sanal makineleri kullanarak hello beklenen performans iyileştirmeleri üretmez.</span><span class="sxs-lookup"><span data-stu-id="4abda-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="4abda-234">Gerekli olduğunda, el ile daha fazla tek çekirdek VM örnekleri ekleyerek ölçeğini veya Otomatik ölçek etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4abda-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="4abda-235">Daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4abda-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="4abda-236">TypeScript ve CoffeeScript desteği</span><span class="sxs-lookup"><span data-stu-id="4abda-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="4abda-237">Doğrudan destek henüz otomatik derleme TypeScript veya CoffeeScript hello çalışma zamanı mevcut olmadığından, bu tür destek dışında hello çalışma zamanı, dağıtım sırasında işlenen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4abda-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4abda-238">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4abda-238">Next steps</span></span>
<span data-ttu-id="4abda-239">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="4abda-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="4abda-240">Azure İşlevleri için en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="4abda-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="4abda-241">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="4abda-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="4abda-242">Azure işlevleri C# Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="4abda-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="4abda-243">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="4abda-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="4abda-244">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="4abda-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

