---
title: "Azure işlevleri için JavaScript Geliştirici Başvurusu | Microsoft Docs"
description: "JavaScript kullanarak işlevleri geliştirmek nasıl anlayın."
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
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="d3030-104">Azure işlevleri JavaScript Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d3030-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3030-105">C# betiği</span><span class="sxs-lookup"><span data-stu-id="d3030-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="d3030-106">F # betiği</span><span class="sxs-lookup"><span data-stu-id="d3030-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="d3030-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d3030-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="d3030-108">Azure işlevleri için JavaScript deneyimi olarak geçirilen bir işlev dışarı aktarmak kolaylaştırır bir `context` alırken ve verileri bağlamaları aracılığıyla gönderme ve çalışma zamanı ile iletişim kurmak için nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="d3030-109">Bu makalede, zaten okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d3030-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="d3030-110">Bir işlev dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d3030-110">Exporting a function</span></span>
<span data-ttu-id="d3030-111">Tüm JavaScript işlevleri tek bir dışarı aktarma `function` aracılığıyla `module.exports` işlevi bulmak ve çalıştırmak çalışma zamanı.</span><span class="sxs-lookup"><span data-stu-id="d3030-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="d3030-112">Bu işlev, her zaman içermelidir bir `context` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d3030-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="d3030-113">Bağlamaları `direction === "in"` boyunca kullanabileceğiniz anlamına gelir işlevi bağımsız geçirilen [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) yeni girişler dinamik olarak işlenecek (kullanarak örneğin, `arguments.length` tüm girişlerinizi yinelemek için).</span><span class="sxs-lookup"><span data-stu-id="d3030-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="d3030-114">Yalnızca bir tetikleyici ve hiçbir ek girişleri varsa başvurulmadan beklendiği tetikleyici verilerinize erişebilir bu işlevi kullanışlı çünkü, `context` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d3030-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="d3030-115">Bağımsız değişkenler her zaman boyunca işlevi içinde gerçekleşme içinde sırayla geçirilir *function.json*dışarı deyiminizde belirtmeyin olsa bile.</span><span class="sxs-lookup"><span data-stu-id="d3030-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="d3030-116">Örneğin, `function(context, a, b)` ve şekilde değiştirin `function(context, a)`, değeri almaya devam `b` başvurma tarafından işlevi kodda `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="d3030-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="d3030-117">Yönü, bağımsız olarak tüm bağlamaları boyunca de geçirilir `context` (aşağıdaki betiği bakın) nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="d3030-118">bağlam nesnesi</span><span class="sxs-lookup"><span data-stu-id="d3030-118">context object</span></span>
<span data-ttu-id="d3030-119">Çalışma zamanı modülünü kullanan bir `context` nesne işlevinizi veri geçirmek için ve çalışma zamanı ile iletişim kurmasına izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="d3030-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="d3030-120">Bağlam nesnesi her zaman ilk parametre bir işlevi olarak ve yöntemleri gibi içerdiğinden dahil edilmelidir `context.done` ve `context.log`, çalışma zamanı doğru bir şekilde kullanmak için gerekli.</span><span class="sxs-lookup"><span data-stu-id="d3030-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="d3030-121">Ne olursa olsun istediğiniz nesne adı verebilirsiniz (örneğin, `ctx` veya `c`).</span><span class="sxs-lookup"><span data-stu-id="d3030-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="d3030-122">Context.Bindings özelliği</span><span class="sxs-lookup"><span data-stu-id="d3030-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="d3030-123">Tüm girdi ve çıktı verilerini içeren adlandırılmış bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="d3030-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="d3030-124">Örneğin, aşağıdaki bağlama tanımında, *function.json* sıradan içeriğini erişim sağlar `context.bindings.myInput` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d3030-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="d3030-125">Context.Done yöntemi</span><span class="sxs-lookup"><span data-stu-id="d3030-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="d3030-126">Kodunuzu bitirdi runtime bildirir.</span><span class="sxs-lookup"><span data-stu-id="d3030-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="d3030-127">Çağırmalısınız `context.done`, veya başka çalışma zamanı hiçbir zaman işlevinizi tamamlandıktan ve yürütme zaman aşımı olur anlar.</span><span class="sxs-lookup"><span data-stu-id="d3030-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="d3030-128">`context.done` Yöntemi geri hem bir kullanıcı tanımlı hata çalışma zamanı ve özellikler üzerine bir özellik paketi özelliklerinin geçirilecek verir `context.bindings` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d3030-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="d3030-129">Context.log yöntemi</span><span class="sxs-lookup"><span data-stu-id="d3030-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="d3030-130">Varsayılan izleme düzeyinde akış konsol günlükleri yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3030-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="d3030-131">Üzerinde `context.log`, ek yöntemleri günlüğü diğer izleme düzeyleri konsol günlüğüne yazmanıza olanak tanıyan kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="d3030-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="d3030-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d3030-132">Method</span></span>                 | <span data-ttu-id="d3030-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d3030-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="d3030-134">**hata (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="d3030-134">**error(_message_)**</span></span>   | <span data-ttu-id="d3030-135">Hata düzeyi oturum açma ya da daha düşük yazar.</span><span class="sxs-lookup"><span data-stu-id="d3030-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="d3030-136">**warn (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="d3030-136">**warn(_message_)**</span></span>    | <span data-ttu-id="d3030-137">Uyarı düzeyi oturum açma ya da daha düşük yazar.</span><span class="sxs-lookup"><span data-stu-id="d3030-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="d3030-138">**bilgi (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="d3030-138">**info(_message_)**</span></span>    | <span data-ttu-id="d3030-139">Oturum açma veya alt bilgi düzeyine yazar.</span><span class="sxs-lookup"><span data-stu-id="d3030-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="d3030-140">**verbose (_ileti_)**</span><span class="sxs-lookup"><span data-stu-id="d3030-140">**verbose(_message_)**</span></span> | <span data-ttu-id="d3030-141">Ayrıntılı düzeyinde günlüğe kaydetme yazar.</span><span class="sxs-lookup"><span data-stu-id="d3030-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="d3030-142">Aşağıdaki örnek, uyarı izleme düzeyinde konsola yazar:</span><span class="sxs-lookup"><span data-stu-id="d3030-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="d3030-143">Host.json dosyasında günlüğe kaydetme için izleme düzeyi eşiğini ayarlayın ya da kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3030-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="d3030-144">Günlüklerine yazma hakkında daha fazla bilgi için sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="d3030-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="d3030-145">Bağlama veri türü</span><span class="sxs-lookup"><span data-stu-id="d3030-145">Binding data type</span></span>

<span data-ttu-id="d3030-146">Bir giriş bağlaması için veri türünü tanımlamak için `dataType` bağlama tanımında özelliği.</span><span class="sxs-lookup"><span data-stu-id="d3030-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="d3030-147">Örneğin, bir HTTP isteği ikili biçimde içeriğini okumak için türü kullanın `binary`:</span><span class="sxs-lookup"><span data-stu-id="d3030-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="d3030-148">Diğer seçenekler için `dataType` olan `stream` ve `string`.</span><span class="sxs-lookup"><span data-stu-id="d3030-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="d3030-149">İzleme çıktısı konsola yazma</span><span class="sxs-lookup"><span data-stu-id="d3030-149">Writing trace output to the console</span></span> 

<span data-ttu-id="d3030-150">İşlevlerde, kullandığınız `context.log` İzleme çıktısı konsola yazma yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="d3030-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="d3030-151">Bu noktada, kullanamazsınız `console.log` konsola yazma.</span><span class="sxs-lookup"><span data-stu-id="d3030-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="d3030-152">Çağırdığınızda `context.log()`, iletinizi olan varsayılan izleme düzeyi konsoluna yazılır _bilgisi_ izleme düzeyi.</span><span class="sxs-lookup"><span data-stu-id="d3030-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="d3030-153">Aşağıdaki kod bilgisi izleme düzeyinde konsola yazar:</span><span class="sxs-lookup"><span data-stu-id="d3030-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="d3030-154">Önceki kod, aşağıdaki kodu eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="d3030-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="d3030-155">Aşağıdaki kod hata düzeyinde konsola yazar:</span><span class="sxs-lookup"><span data-stu-id="d3030-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="d3030-156">Çünkü _hata_ yüksek izleme günlüğü etkin olduğu sürece düzeyi, bu izleme çıktısı tüm izleme düzeylerde yazılır.</span><span class="sxs-lookup"><span data-stu-id="d3030-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="d3030-157">Tüm `context.log` yöntemlerini desteklemek Node.js tarafından desteklenen aynı parametre biçimi [util.format yöntemi](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="d3030-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="d3030-158">Varsayılan izleme düzeyi kullanarak konsola aşağıdaki kodu göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d3030-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="d3030-159">Ayrıca, aynı kod şu biçimde yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d3030-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="d3030-160">Konsol günlüğe kaydetme için izleme düzeyini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d3030-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="d3030-161">İşlevler şekilde izlemeleri, işlevlerden konsoluna yazılan denetim kolay hale getirir konsola yazma için eşik izleme düzeyi tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3030-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="d3030-162">Konsola yazılan tüm izlemeleri eşiği ayarlamak için kullanın `tracing.consoleLevel` host.json dosyasında özellik.</span><span class="sxs-lookup"><span data-stu-id="d3030-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="d3030-163">Bu ayar, tüm işlevlere işlevi uygulamanızda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d3030-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="d3030-164">Aşağıdaki örnek, ayrıntılı günlük kaydını etkinleştirmek için izleme eşik ayarlar:</span><span class="sxs-lookup"><span data-stu-id="d3030-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="d3030-165">Değerleri **consoleLevel** adları için karşılık gelen `context.log` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="d3030-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="d3030-166">Konsola tüm izleme günlüğü devre dışı bırakmak için ayarlanmış **consoleLevel** için _devre dışı_.</span><span class="sxs-lookup"><span data-stu-id="d3030-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="d3030-167">Host.json dosyası hakkında daha fazla bilgi için bkz: [host.json başvuru konusu](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="d3030-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="d3030-168">HTTP Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="d3030-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="d3030-169">HTTP ve Web kancası Tetikleyicileri ve bağlamaları istek ve yanıt nesneleri HTTP ileti temsil etmek için kullanır. çıktı.</span><span class="sxs-lookup"><span data-stu-id="d3030-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="d3030-170">İstek nesnesi</span><span class="sxs-lookup"><span data-stu-id="d3030-170">Request object</span></span>

<span data-ttu-id="d3030-171">`request` Nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d3030-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="d3030-172">Özellik</span><span class="sxs-lookup"><span data-stu-id="d3030-172">Property</span></span>      | <span data-ttu-id="d3030-173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d3030-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="d3030-174">_Gövde_</span><span class="sxs-lookup"><span data-stu-id="d3030-174">_body_</span></span>        | <span data-ttu-id="d3030-175">İstek gövdesini içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="d3030-176">_üstbilgileri_</span><span class="sxs-lookup"><span data-stu-id="d3030-176">_headers_</span></span>     | <span data-ttu-id="d3030-177">İstek üstbilgilerini içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="d3030-178">_yöntemi_</span><span class="sxs-lookup"><span data-stu-id="d3030-178">_method_</span></span>      | <span data-ttu-id="d3030-179">İsteğin HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d3030-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="d3030-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="d3030-180">_originalUrl_</span></span> | <span data-ttu-id="d3030-181">İstek URL'si.</span><span class="sxs-lookup"><span data-stu-id="d3030-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="d3030-182">_parametreleri_</span><span class="sxs-lookup"><span data-stu-id="d3030-182">_params_</span></span>      | <span data-ttu-id="d3030-183">İsteğin Yönlendirme parametreleri içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="d3030-184">_Sorgu_</span><span class="sxs-lookup"><span data-stu-id="d3030-184">_query_</span></span>       | <span data-ttu-id="d3030-185">Sorgu parametreleri içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="d3030-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="d3030-186">_rawBody_</span></span>     | <span data-ttu-id="d3030-187">Dize olarak ileti gövdesi.</span><span class="sxs-lookup"><span data-stu-id="d3030-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="d3030-188">Yanıt nesnesi</span><span class="sxs-lookup"><span data-stu-id="d3030-188">Response object</span></span>

<span data-ttu-id="d3030-189">`response` Nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d3030-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="d3030-190">Özellik</span><span class="sxs-lookup"><span data-stu-id="d3030-190">Property</span></span>  | <span data-ttu-id="d3030-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d3030-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="d3030-192">_Gövde_</span><span class="sxs-lookup"><span data-stu-id="d3030-192">_body_</span></span>    | <span data-ttu-id="d3030-193">Yanıtın gövdesini içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="d3030-194">_üstbilgileri_</span><span class="sxs-lookup"><span data-stu-id="d3030-194">_headers_</span></span> | <span data-ttu-id="d3030-195">Yanıt üst bilgileri içeren bir nesne.</span><span class="sxs-lookup"><span data-stu-id="d3030-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="d3030-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="d3030-196">_isRaw_</span></span>   | <span data-ttu-id="d3030-197">Biçimlendirme için yanıt atlanır gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3030-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="d3030-198">_durumu_</span><span class="sxs-lookup"><span data-stu-id="d3030-198">_status_</span></span>  | <span data-ttu-id="d3030-199">Yanıtının HTTP durum kodu.</span><span class="sxs-lookup"><span data-stu-id="d3030-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="d3030-200">İstek ve yanıt erişme</span><span class="sxs-lookup"><span data-stu-id="d3030-200">Accessing the request and response</span></span> 

<span data-ttu-id="d3030-201">HTTP tetikleyicileri ile çalışırken, HTTP istek ve yanıt nesneleri herhangi üç yolla erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d3030-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="d3030-202">Adlandırılmış giriş ve çıkış bağlamaları.</span><span class="sxs-lookup"><span data-stu-id="d3030-202">From the named input and output bindings.</span></span> <span data-ttu-id="d3030-203">Bu şekilde, HTTP tetikleyicisini ve bağlamaları başka bir bağlama ile aynı çalışır.</span><span class="sxs-lookup"><span data-stu-id="d3030-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="d3030-204">Aşağıdaki örnek, bir adlandırılmış kullanarak yanıt nesnesini ayarlar `response` bağlama:</span><span class="sxs-lookup"><span data-stu-id="d3030-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="d3030-205">Gelen `req` ve `res` özellikleri `context` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d3030-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="d3030-206">Bu şekilde, geleneksel düzeni verilere erişmek HTTP için tam kullanmak zorunda olmak yerine bağlam nesnesinden kullanabileceğiniz `context.bindings.name` düzeni.</span><span class="sxs-lookup"><span data-stu-id="d3030-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="d3030-207">Aşağıdaki örnekte nasıl erişeceğinizi gösterir `req` ve `res` üzerinde nesneleri `context`:</span><span class="sxs-lookup"><span data-stu-id="d3030-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="d3030-208">Çağırarak `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="d3030-208">By calling `context.done()`.</span></span> <span data-ttu-id="d3030-209">Özel türde bir HTTP bağlaması için geçirilen yanıtı döndürür `context.done()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d3030-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="d3030-210">Aşağıdaki HTTP bağlama çıktı tanımlayan bir `$return` çıkış parametresi:</span><span class="sxs-lookup"><span data-stu-id="d3030-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="d3030-211">Bu çıktı bağlama, çağırdığınızda yanıt vermesini bekliyor `done()`aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="d3030-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="d3030-212">Düğüm sürümü ve paket Yönetimi</span><span class="sxs-lookup"><span data-stu-id="d3030-212">Node version and Package Management</span></span>
<span data-ttu-id="d3030-213">Düğüm sürüm adresindeki kilitli `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="d3030-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="d3030-214">Geçerli daha fazla sürümleri için destek eklenmesi araştırma, yapılandırılabilir hale getirme.</span><span class="sxs-lookup"><span data-stu-id="d3030-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="d3030-215">Aşağıdaki adımları işlevi uygulamanızda paketleri dahil sağlar:</span><span class="sxs-lookup"><span data-stu-id="d3030-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="d3030-216">`https://<function_app_name>.scm.azurewebsites.net` kısmına gidin.</span><span class="sxs-lookup"><span data-stu-id="d3030-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="d3030-217">Tıklatın **Debug konsol** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="d3030-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="d3030-218">Git `D:\home\site\wwwroot`, package.json dosyanızı sürükleyin **wwwroot** sayfanın üst yarısındaki klasörü.</span><span class="sxs-lookup"><span data-stu-id="d3030-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="d3030-219">Dosya başka yollarla işlevi uygulamanıza da karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3030-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="d3030-220">Daha fazla bilgi için bkz: [işlevi uygulama dosyaları güncelleştirmek nasıl](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="d3030-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="d3030-221">Package.json dosyası karşıya yüklendikten sonra çalıştırmak `npm install` komutunu **Kudu uzaktan yürütme konsol**.</span><span class="sxs-lookup"><span data-stu-id="d3030-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="d3030-222">Bu eylem package.json dosyasında belirtilen paket indirir ve işlev uygulaması yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="d3030-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="d3030-223">Gereksinim duyduğunuz paketleri yüklendikten sonra işleve çağırarak aldıktan `require('packagename')`, aşağıdaki örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="d3030-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="d3030-224">Tanımlamanız gerekir bir `package.json` işlevi uygulamanızın kök dizinindeki dosyasını.</span><span class="sxs-lookup"><span data-stu-id="d3030-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="d3030-225">Dosya tanımlama aynı önbelleğe alınmış paketleri, en iyi performans sağlayan paylaşmak uygulamasında tüm işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3030-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="d3030-226">Sürüm çakışması ortaya çıkarsa, ekleyerek çözebilmek bir `package.json` belirli bir işlev klasöründe bulunan dosyadır.</span><span class="sxs-lookup"><span data-stu-id="d3030-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="d3030-227">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="d3030-227">Environment variables</span></span>
<span data-ttu-id="d3030-228">Bir ortam değişkeni veya ayar değeri bir uygulamayı almak için `process.env`aşağıdaki kod örneğinde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="d3030-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="d3030-229">JavaScript işlevleri için ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="d3030-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="d3030-230">JavaScript işlevleri ile çalışırken, aşağıdaki iki bölümlerdeki konuları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d3030-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="d3030-231">Tek çekirdekli uygulama hizmeti planları seçin</span><span class="sxs-lookup"><span data-stu-id="d3030-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="d3030-232">Uygulama hizmeti planı kullanan bir işlev uygulaması oluşturduğunuzda, bir plan ile birden çok çekirdek yerine bir tek çekirdek planı seçmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="d3030-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="d3030-233">Bugün, işlevleri çalışır JavaScript işlevleri daha verimli bir şekilde tek çekirdekli sanal makineler ve büyük sanal makineleri kullanarak beklenen performans iyileştirmeleri üretmez.</span><span class="sxs-lookup"><span data-stu-id="d3030-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="d3030-234">Gerekli olduğunda, el ile daha fazla tek çekirdek VM örnekleri ekleyerek ölçeğini veya Otomatik ölçek etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3030-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="d3030-235">Daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3030-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="d3030-236">TypeScript ve CoffeeScript desteği</span><span class="sxs-lookup"><span data-stu-id="d3030-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="d3030-237">Doğrudan destek henüz otomatik derleme TypeScript veya CoffeeScript için çalışma zamanı mevcut olmadığından, bu tür destek dışında çalışma zamanı, dağıtım sırasında yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3030-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d3030-238">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3030-238">Next steps</span></span>
<span data-ttu-id="d3030-239">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="d3030-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="d3030-240">Azure İşlevleri için en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d3030-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="d3030-241">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="d3030-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="d3030-242">Azure işlevleri C# Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="d3030-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="d3030-243">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="d3030-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="d3030-244">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="d3030-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

