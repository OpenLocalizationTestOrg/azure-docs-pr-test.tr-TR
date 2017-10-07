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
# <a name="azure-functions-javascript-developer-guide"></a>Azure işlevleri JavaScript Geliştirici Kılavuzu
> [!div class="op_single_selector"]
> * [C# betiği](functions-reference-csharp.md)
> * [F # betiği](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Azure işlevleri kolaylaştırır kolay tooexport olarak geçirilen bir işlev için JavaScript deneyimi hello bir `context` alırken ve verileri bağlamaları aracılığıyla gönderme ve hello çalışma zamanı ile iletişim kurmak için nesne.

Bu makalede, zaten hello okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).

## <a name="exporting-a-function"></a>Bir işlev dışarı aktarma
Tüm JavaScript işlevleri tek bir dışarı aktarma `function` aracılığıyla `module.exports` hello çalışma zamanı için toofind hello işlevi ve çalıştırın. Bu işlev, her zaman içermelidir bir `context` nesnesi.

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

Bağlamaları `direction === "in"` boyunca kullanabileceğiniz anlamına gelir işlevi bağımsız geçirilen [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically işlemek yeni girişleri (kullanarak örneğin, `arguments.length` tooiterate tüm girişlerinizi üzerinden). Yalnızca bir tetikleyici ve hiçbir ek girişleri varsa başvurulmadan beklendiği tetikleyici verilerinize erişebilir bu işlevi kullanışlı çünkü, `context` nesnesi.

Merhaba bağımsız değişkenleri toohello işlevi içinde gerçekleşme içinde hello sırayla boyunca her zaman geçirilir *function.json*dışarı deyiminizde belirtmeyin olsa bile. Örneğin, `function(context, a, b)` ve çok değiştirme`function(context, a)`, hello değerini almaya devam `b` çok başvuran tarafından işlevi kodda`arguments[3]`.

Yönü, bağımsız olarak tüm bağlamaları ayrıca boyunca üzerinde hello geçirilen `context` (komut dosyası izleyen hello bakın) nesne. 

## <a name="context-object"></a>bağlam nesnesi
Merhaba çalışma zamanı modülünü kullanan bir `context` nesne toopass veri tooand işlevi ve toolet hello çalışma zamanı ile iletişim kurar.

Merhaba bağlam nesnesi her zaman hello ilk parametre tooa işlev ve yöntemleri gibi içerdiğinden dahil edilmelidir `context.done` ve `context.log`, olan gerekli toouse hello çalışma zamanı doğru. Ne olursa olsun ister misiniz hello nesne adı verebilirsiniz (örneğin, `ctx` veya `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>Context.Bindings özelliği

```
context.bindings
```
Tüm girdi ve çıktı verilerini içeren adlandırılmış bir nesne döndürür. Örneğin, bağlama tanımı'nda aşağıdaki Merhaba, *function.json* size erişim sağlar hello hello hello sıradan içeriğini `context.bindings.myInput` nesnesi. 

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

### <a name="contextdone-method"></a>Context.Done yöntemi
```
context.done([err],[propertyBag])
```

Kodunuzu bitirdi hello çalışma zamanı bildirir. Çağırmalısınız `context.done`, veya başka hello çalışma zamanı hiçbir zaman bilir işlevinizi tamamlandıktan ve hello yürütme zaman aşımı olur. 

Merhaba `context.done` yöntemi sağlar, toopass başa bir kullanıcı tanımlı hata toohello çalışma zamanı ve bir özellik paketi hello hello özellikleri üzerine özelliklerinin `context.bindings` nesnesi.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>Context.log yöntemi  

```
context.log(message)
```
Toowrite toohello akış konsol günlükleri hello varsayılan izleme düzeyinde sağlar. Üzerinde `context.log`, ek yöntemleri günlüğü toohello konsol günlüğüne diğer izleme düzeyleri yazmanıza olanak tanıyan kullanılabilir:


| Yöntem                 | Açıklama                                |
| ---------------------- | ------------------------------------------ |
| **hata (_ileti_)**   | Oturum açma veya alt tooerror düzeyinde yazar.   |
| **warn (_ileti_)**    | Oturum açma veya alt toowarning düzeyinde yazar. |
| **bilgi (_ileti_)**    | Oturum açma veya alt tooinfo düzeyinde yazar.    |
| **verbose (_ileti_)** | Tooverbose düzeyinde günlüğe kaydetme yazar.           |

Merhaba aşağıdaki örnek hello uyarı izleme düzeyi toohello konsolda Yazar:

```javascript
context.log.warn("Something has happened."); 
```
Merhaba host.json dosyasında günlüğe kaydetme için hello izleme düzeyi eşiğini ayarlayın ya da kapatabilirsiniz.  Nasıl toowrite toohello günlükleri hakkında daha fazla bilgi için hello sonraki bölümüne bakın.

## <a name="binding-data-type"></a>Bağlama veri türü

toodefine hello kullanmak için bir giriş bağlama, hello veri türü `dataType` hello bağlama tanımında özelliği. Örneğin, tooread ikili biçimde bir HTTP isteğinin içerik Merhaba, hello türünü kullanmak `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Diğer seçenekler için `dataType` olan `stream` ve `string`.

## <a name="writing-trace-output-toohello-console"></a>Yazma İzleme çıktısı toohello konsol 

İşlevlerde, kullandığınız hello `context.log` yöntemleri toowrite İzleme çıktısı toohello konsol. Bu noktada, kullanamazsınız `console.log` toowrite toohello konsol.

Çağırdığınızda `context.log()`, iletinizi hello olduğu hello varsayılan izleme düzeyi toohello konsolda yazılır _bilgisi_ izleme düzeyi. Merhaba aşağıdaki kod hello bilgi izleme düzeyini toohello konsolda Yazar:

```javascript
context.log({hello: 'world'});  
```

Hello önceki kod eşdeğer toohello kod aşağıdaki gibidir:

```javascript
context.log.info({hello: 'world'});  
```

Merhaba aşağıdaki kod toohello konsol hello hata düzeyinde Yazar:

```javascript
context.log.error("An error has occurred.");  
```

Çünkü _hata_ hello yüksek izleme günlüğü etkin olduğu sürece düzeyi, bu izleme toohello çıktısı tüm izleme düzeylerde yazılır.  


Tüm `context.log` yöntemlerini desteklemek hello Node.js hello tarafından desteklenen aynı parametre biçimi [util.format yöntemi](https://nodejs.org/api/util.html#util_util_format_format). Merhaba varsayılan izleme düzeyi kullanarak toohello konsol yazar kod aşağıdaki hello göz önünde bulundurun:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

Ayrıca, aynı hello biçimini izleyen kod yazma hello de yapabilirsiniz:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Konsol günlüğe kaydetme için Hello izleme düzeyini yapılandırın

İşlevler izlemeleri, işlevlerden toohello konsol yazılır kolay toocontrol hello şekilde kolaylaştırır toohello konsol yazma hello eşik izleme düzeyi tanımlamanıza olanak sağlar. tooset hello eşik toohello konsol, kullanım hello yazılan tüm izlemeleri için `tracing.consoleLevel` hello host.json dosyasında özellik. Bu ayar işlevi uygulamanızı tooall işlevlerinde geçerlidir. Merhaba aşağıdaki örnek hello izleme eşik tooenable ayrıntılı günlük kaydını ayarlar:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Değerleri **consoleLevel** hello toohello adlarını karşılık `context.log` yöntemleri. Tüm izleme toohello konsol oturum toodisable ayarlamak **consoleLevel** too_off_. Merhaba hello host.json dosyası hakkında daha fazla bilgi için bkz: [host.json başvuru konusu](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>HTTP Tetikleyicileri ve bağlamaları

HTTP ve Web kancası Tetikleyicileri ve bağlamaları istek ve yanıt nesneleri toorepresent hello HTTP Mesajlaşma kullanmak çıktı.  

### <a name="request-object"></a>İstek nesnesi

Merhaba `request` nesnesi hello aşağıdaki özelliklere sahiptir:

| Özellik      | Açıklama                                                    |
| ------------- | -------------------------------------------------------------- |
| _Gövde_        | Merhaba hello istek gövdesini içeren bir nesne.               |
| _üstbilgileri_     | Merhaba istek üstbilgileri içeren bir nesne.                   |
| _yöntemi_      | Merhaba hello isteğinin HTTP yöntemi.                                |
| _originalUrl_ | Merhaba isteği Hello URL'si.                                        |
| _parametreleri_      | Merhaba isteğinin hello Yönlendirme parametreleri içeren bir nesne. |
| _Sorgu_       | Merhaba sorgu parametreleri içeren bir nesne.                  |
| _rawBody_     | dize olarak hello ileti gövdesi Hello.                           |


### <a name="response-object"></a>Yanıt nesnesi

Merhaba `response` nesnesi hello aşağıdaki özelliklere sahiptir:

| Özellik  | Açıklama                                               |
| --------- | --------------------------------------------------------- |
| _Gövde_    | Merhaba hello yanıtın gövdesini içeren bir nesne.         |
| _üstbilgileri_ | Merhaba yanıt üst bilgileri içeren bir nesne.             |
| _isRaw_   | Biçimlendirme için hello yanıt atlanır gösterir.    |
| _durumu_  | Merhaba hello yanıtının HTTP durum kodu.                     |

### <a name="accessing-hello-request-and-response"></a>Merhaba istek ve yanıt erişme 

HTTP tetikleyicileri ile çalışırken, herhangi bir üç şekilde hello HTTP istek ve yanıt nesneleri erişebilirsiniz:

+ Giriş Hello adlı ve bağlamaları çıktı. Bu şekilde, hello HTTP tetikleyici ve bağlamaları iş aynı herhangi bir bağlama olarak hello. Merhaba aşağıdaki örnek hello yanıt nesnesi bir adlandırılmış kullanarak ayarlar `response` bağlama: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ Gelen `req` ve `res` hello özellikleri `context` nesnesi. Bu şekilde, toouse hello tam sahip olmak yerine hello geleneksel düzeni tooaccess HTTP hello bağlam nesnesi, verilerden kullanabilirsiniz `context.bindings.name` düzeni. örnekte gösterildiği nasıl aşağıdaki hello tooaccess hello `req` ve `res` hello nesnelerde `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Çağırarak `context.done()`. Özel türde bir HTTP bağlaması toohello geçirilen hello yanıtı döndürür `context.done()` yöntemi. HTTP aşağıdaki hello çıktı bağlama tanımlayan bir `$return` çıkış parametresi:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    Bu çıktı bağlama çağırdığınızda toosupply hello yanıt bekliyor `done()`aşağıdaki gibi:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Düğüm sürümü ve paket Yönetimi
Merhaba düğümü sürüm şu anda kilitli `6.5.0`. Geçerli daha fazla sürümleri için destek eklenmesi araştırma, yapılandırılabilir hale getirme.

Aşağıdaki adımları hello işlevi uygulamanızda paketleri dahil sağlar: 

1. Çok Git`https://<function_app_name>.scm.azurewebsites.net`.

2. Tıklatın **Debug konsol** > **CMD**.

3. Çok Git`D:\home\site\wwwroot`, package.json dosyası toohello sürükleyin **wwwroot** hello sayfasının üst yarı hello klasörü.  
    Dosyaları tooyour işlev uygulaması başka yöntemler de yükleyebilirsiniz. Daha fazla bilgi için bkz: [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate). 

4. Merhaba package.json dosyası karşıya yüklendikten sonra hello çalıştırmak `npm install` hello komutunu **Kudu uzaktan yürütme konsol**.  
    Bu eylem hello package.json dosyasında belirtildiği hello paketleri indirir ve hello işlev uygulaması yeniden başlatır.

Merhaba ihtiyacınız paketleri yüklendikten sonra bunları tooyour işlevi çağırarak aldığınız `require('packagename')`, aşağıdaki örneğine hello olarak:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

Tanımlamanız gerekir bir `package.json` dosya işlevi uygulamanızın hello kökü. Tanımlama hello dosya aynı önbelleğe alınan paketler hello en iyi performans sağlayan hello hello uygulama paylaşım uygulamasında tüm işlevleri sağlar. Sürüm çakışması ortaya çıkarsa, ekleyerek çözebilmek bir `package.json` belirli bir işlev hello klasöründe bulunan dosyadır.  

## <a name="environment-variables"></a>Ortam değişkenleri
tooget bir ortam değişkeni veya kullanan bir uygulama ayarı değeri `process.env`, aşağıdaki kod örneğine hello gösterildiği gibi:

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
## <a name="considerations-for-javascript-functions"></a>JavaScript işlevleri için ilgili önemli noktalar

JavaScript işlevleri ile çalışırken, iki bölüme aşağıdaki hello hello konuları farkında olması.

### <a name="choose-single-core-app-service-plans"></a>Tek çekirdekli uygulama hizmeti planları seçin

Merhaba uygulama hizmeti planı kullanan bir işlev uygulaması oluşturduğunuzda, bir plan ile birden çok çekirdek yerine bir tek çekirdek planı seçmenizi öneririz. Bugün, işlevleri çalışır JavaScript işlevleri daha verimli bir şekilde tek çekirdekli sanal makineler ve büyük sanal makineleri kullanarak hello beklenen performans iyileştirmeleri üretmez. Gerekli olduğunda, el ile daha fazla tek çekirdek VM örnekleri ekleyerek ölçeğini veya Otomatik ölçek etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>TypeScript ve CoffeeScript desteği
Doğrudan destek henüz otomatik derleme TypeScript veya CoffeeScript hello çalışma zamanı mevcut olmadığından, bu tür destek dışında hello çalışma zamanı, dağıtım sırasında işlenen toobe gerekir. 

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Azure İşlevleri için en iyi uygulamalar](functions-best-practices.md)
* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)
* [Azure işlevleri C# Geliştirici Başvurusu](functions-reference-csharp.md)
* [Azure işlevleri F # Geliştirici Başvurusu](functions-reference-fsharp.md)
* [Azure işlevleri Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md)

