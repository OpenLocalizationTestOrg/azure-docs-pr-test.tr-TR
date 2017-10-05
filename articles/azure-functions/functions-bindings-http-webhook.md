---
title: "Azure işlevleri HTTP ve Web kancası bağlamaları | Microsoft Docs"
description: "HTTP ve Web kancası Tetikleyicileri ve bağlamaları Azure işlevlerinde nasıl kullanılacağını anlayın."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme, Web kancalarını, dinamik, sunucusuz mimarisi, HTTP, API REST işlem"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Azure işlevleri HTTP ve Web kancası bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede, yapılandırma ve HTTP Tetikleyicileri ve bağlamaları Azure işlevlerinde çalışmak açıklanmaktadır.
Bu konularda sunucusuz API'ları derleme ve Web kancası için yanıt vermek için Azure işlevleri kullanabilirsiniz.

Azure işlevleri aşağıdaki bağlamaları sağlar:
- Bir [HTTP tetikleyicisini](#httptrigger) bir HTTP isteğiyle bir işlevi çağırmak olanak tanır. Bu yanıt için özelleştirilebilir [kancalarını](#hooktrigger).
- Bir [HTTP bağlama çıktı](#output) isteğine yanıt olanak tanır.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>HTTP tetikleyicisi
HTTP tetikleyicisini işlevinizde bir HTTP isteğine yanıt olarak yürütülür. Belirli bir URL veya HTTP yöntemleri kümesini yanıt verecek şekilde özelleştirebilirsiniz. Bir HTTP tetikleyicisi için Web kancası yanıt verecek şekilde de yapılandırılabilir. 

İşlevler Portalı'nı kullanarak, siz de hemen önceden yapılmış bir şablon kullanarak başlayabiliriz. Seçin **yeni işlev** ve "API & Web Kancalarını" arasından **senaryo** açılır. Şablonlardan birini seçin ve tıklatın **oluşturma**.

Varsayılan olarak, bir HTTP tetikleyicisi bir HTTP 200 Tamam durum kodu ve boş bir gövde ile isteğine yanıt verir. Yanıt değiştirmek için yapılandırma bir [HTTP çıktı bağlama](#output)

### <a name="configuring-an-http-trigger"></a>Bir HTTP tetikleyicisi yapılandırma
Bir HTTP tetikleyicisi aşağıdakine benzer bir JSON nesnesi de dahil olmak üzere tarafından tanımlanan `bindings` function.json dizisi:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
Bağlama aşağıdaki özellikleri destekler:

* **ad** : gerekli - istek veya istek gövdesi için işlevi kod içinde kullanılan değişken adı. Bkz: [bir HTTP tetikleyicisi koddan çalışan](#httptriggerusage).
* **tür** : gerekli - "httpTrigger" ayarlanması gerekir.
* **Yön** : gerekli - "için" kümesindeki olması gerekir.
* _authLevel_ : Bu anahtarları, varsa, işlevin çalıştırılabilmesi için istekte bulunması gerekenleri belirler. Bkz: [anahtarlarla çalışma](#keys) aşağıda. Değerin aşağıdakilerden biri olabilir:
    * _Anonim_: Hayır API anahtarı gereklidir.
    * _işlev_: bir işleve özgü API anahtarı gereklidir. Bu, hiçbiri sağlanmazsa varsayılan değerdir.
    * _Yönetici_ : ana anahtar gereklidir.
* **yöntemleri** : Bu işlev yanıt için HTTP yöntemleri dizisidir. Belirtilmezse, işlev tüm HTTP yöntemlerine yanıt verir. Bkz: [HTTP uç noktası özelleştirme](#url).
* **Rota** : Bu rota şablonu tanımlar, kendisine URL'leri isteği denetleme işlevinizin yanıt verir. Varsayılan değer hiçbiri sağlanmazsa `<functionname>`. Bkz: [HTTP uç noktası özelleştirme](#url).
* **webHookType** : Bu, HTTP tetikleyicisini belirtilen sağlayıcı için bir Web kancası reciever davranacak şekilde yapılandırır. _Yöntemleri_ özelliği, değil Bu seçilirse ayarlanmalıdır. Bkz: [Web kancası için yanıt](#hooktrigger). Değerin aşağıdakilerden biri olabilir:
    * _genericJson_ : belirli bir sağlayıcı için mantığı olmadan bir genel amaçlı Web kancası uç noktası.
    * _github_ : işlevi için GitHub Web kancası yanıt verir. _AuthLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.
    * _kayma_ : işlevi Slack kancalarını yanıt verir. _AuthLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Bir HTTP tetikleyicisi kodu ile çalışma
C# ve F # işlevleri için giriş aşağıdakilerden biri olması için tetikleyici türünü bildirebilir `HttpRequestMessage` veya özel bir tür. Seçerseniz `HttpRequestMessage`, istek nesnesi tam erişimi alırsınız. İçin özel bir tür (örneğin, bir POCO) işlevleri istek gövdesi nesne özelliklerini doldurmak için JSON olarak ayrıştırılamıyor dener.

Node.js işlevleri için işlevleri çalışma zamanı yerine request nesnesi istek gövdesinde sağlar.

Bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) örneğin kullanımları.


<a name="output"></a>
## <a name="http-response-output-binding"></a>HTTP yanıtının çıkış bağlama
HTTP isteği gönderene yanıt bağlama HTTP çıkış kullanın. Bu bağlamanın bir HTTP tetikleyicisi gerektirir ve tetikleyici istekle ilişkili yanıt özelleştirmenizi sağlar. Bir HTTP bağlaması çıktı bir HTTP tetikleyicisi boş bir gövde ile HTTP 200 Tamam döndürmeyecektir sağlanan olur. 

### <a name="configuring-an-http-output-binding"></a>Bir HTTP yapılandırma bağlama çıktı
HTTP çıkış bağlama aşağıdakine benzer bir JSON nesnesi ekleyerek tanımlanmış `bindings` function.json dizisi:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
Bağlama aşağıdaki özellikleri içerir:

* **ad** : gerekli - yanıt işlevi kod içinde kullanılan değişken adı. Bkz: [bir HTTP ile çalışma çıktı kodundan bağlama](#outputusage).
* **tür** : gerekli - "http" olarak ayarlanması gerekir.
* **Yön** : gerekli - out"için" ayarlanması gerekir.

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Bir HTTP ile çalışma kodundan bağlama çıktı
Http veya Web kancası çağırana yanıt için çıktı parametresi (örneğin, "res") kullanabilirsiniz. Alternatif olarak, standart kullanabilirsiniz `Request.CreateResponse()` (C#) veya `context.res` yanıtınız döndürülecek (Node.JS) deseni. İkinci yöntemi kullanma hakkında daha fazla örnekler için bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) ve [Web kancası tetikleyici örnekleri](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a>Web kancası için yanıt
Bir HTTP tetikleyicisi ile _webHookType_ özelliği, yanıt verecek şekilde yapılandırılacak [kancalarını](https://en.wikipedia.org/wiki/Webhook). Temel yapılandırma "genericJson" ayarını kullanır. Bu istekleri yalnızca HTTP POST ile ile kısıtlayan `application/json` içerik türü.

Tetikleyici için bir özel Web kancası sağlayıcısı ayrıca uyarlanabilir (örn., [GitHub](https://developer.github.com/webhooks/) ve [Slack'e](https://api.slack.com/outgoing-webhooks)). Bir sağlayıcı belirtilmemişse işlevleri çalışma zamanı sağlayıcının doğrulama mantığını sizin için dikkatli olun.  

### <a name="configuring-github-as-a-webhook-provider"></a>GitHub Web kancası sağlayıcısı olarak yapılandırma
GitHub Web kancası için yanıt vermek için önce bir HTTP tetikleyicisi ile işlevinizi oluşturma ve ayarlama _webHookType_ "github" özelliğine. Ardından kopyalama kendi [URL](#url) ve [API anahtarı](#keys) GitHub deponun içine **Web kancası eklemek** sayfası. GitHub'ınızın bkz [Web kancası oluşturma](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) daha fazla bilgi için belgeleri.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Bir Web kancası sağlayıcısı olarak kayma yapılandırma
Slack Web kancası işlevi özel bir anahtar kayma belirtecinden ile yapılandırmanız gerekir, belirtmenize izin verir yerine bir belirteç sizin için oluşturur. Bkz: [anahtarlarla çalışma](#keys).

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a>HTTP uç noktası özelleştirme
Bir HTTP tetikleyicisi ya da Web kancası, bir işlev oluşturduğunuzda varsayılan olarak işlevi adreslenebilir biçiminde bir yol şu şekildedir:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

İsteğe bağlı kullanarak bu yolun özelleştirebilirsiniz `route` HTTP tetikleyicisini özellikte bağlama girdisini. Örneğin, aşağıdaki *function.json* dosya tanımlayan bir `route` özelliği bir HTTP tetikleyicisi için:

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

Bu yapılandırma, işlevi artık özgün yol yerine aşağıdaki yol ile adreslenebilir kullanmaktır.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Bu adres, "kategorisi" ve "id" iki parametrelerini desteklemek işlev kodu sağlar. Kullanabilirsiniz [Web API rota kısıtlaması](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) , parametrelere sahip. Aşağıdaki C# işlevi kodu her iki parametrelerini kullanır.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Burada, aynı rota parametrelerini kullanmak için Node.js işlev kodu verilmiştir.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

Varsayılan olarak, tüm işlevi yollar ile önek *API*. Ayrıca özelleştirme veya önek kullanarak kaldırma `http.routePrefix` özelliğinde, *host.json* dosya. Aşağıdaki örnek kaldırır *API* önekini için boş bir dize kullanarak rota öneki *host.json* dosya.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Güncelleştirme hakkında ayrıntılı bilgi için *host.json* bakın, işlevinizi dosyası [işlevi uygulama dosyaları güncelleştirmek nasıl](functions-reference.md#fileupdate). 

Diğer özellikler hakkında bilgi için yapılandırabileceğiniz, *host.json* dosya için bkz: [host.json başvuru](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Anahtarları ile çalışma
HttpTriggers ek güvenlik için anahtarları yararlanabilirsiniz. Standart HttpTrigger istekte bulunması için anahtar gerektiren bir API anahtarı olarak kullanabilirsiniz. Web kancası bir ne sağlayıcının desteklediği bağlı olarak, çeşitli şekillerde isteklerinde yetkilendirmek için tuşlarını kullanabilirsiniz.

Anahtarları azure'da işlevi uygulamanız bir parçası olarak depolanır ve bekleyen şifrelenir. Anahtarlarınızı görüntülemek için yeni bir tane oluşturun veya anahtarları alma yeni değerler, işlevlerinizi portalındaki birine gidin ve "Manage" seçin 

Anahtarların iki tür vardır:
- **Ana bilgisayar anahtarları**: Bu anahtarları işlevi uygulamasında tüm işlevleri tarafından paylaşılır. Bir API anahtarı olarak kullanıldığında, bu işlev uygulaması içinde herhangi bir işlev erişime izin verin.
- **İşlev tuşları**: Bu anahtarları altında bunların tanımlanan yalnızca belirli işlevler için geçerlidir. Bunlar yalnızca, bir API anahtarı olarak kullanıldığında, bu işlev erişime izin ver.

Her anahtar için başvuru olarak adlandırılır ve işlev ve ana bilgisayar düzeyinde ("varsayılan" adlı) bir varsayılan anahtar yok. **Ana anahtar** varsayılan ana bilgisayar anahtarı "her işlev uygulaması için tanımlanır ve iptal edilemiyor _master" olarak adlandırılmıştır. Çalışma zamanı API yönetim erişim sağlar. Kullanarak `"authLevel": "admin"` bağlamasında JSON isteği sunulması için bu anahtar gerekir; başka bir anahtar bir yetkilendirme hatasına neden olur.

> [!NOTE]
> Ana anahtar ile yükseltilmiş izinler nedeniyle, bu anahtarı üçüncü taraflarla paylaşma veya gerekir yerel istemci uygulamalarında dağıtın. Yönetici yetki düzeyini seçerken dikkatli olun.
> 
> 

### <a name="api-key-authorization"></a>API anahtarı yetkilendirme
Varsayılan olarak, bir HttpTrigger HTTP isteği bir API anahtarı gerektirir. Bu nedenle, HTTP isteği normalde şöyle görünür:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

Anahtar adlı bir sorgu dizesi değişkeni dahil edilebilir `code`, yukarıdaki olarak veya içinde eklenebilir bir `x-functions-key` HTTP üstbilgisi. Anahtarın değerini işlevi için tanımlanan herhangi bir işlev tuşu veya tüm ana bilgisayar anahtarı olabilir.

Anahtarları olmadan isteklere izin vermek veya ana anahtarı değiştirerek kullanılması gerektiğini belirtmek seçebileceğiniz `authLevel` JSON bağlama özelliğinde (bkz [HTTP tetikleyicisini](#httptrigger)).

### <a name="keys-and-webhooks"></a>Anahtarlar ve Web kancaları
Web kancası yetkilendirme Web kancası reciever bileşeni tarafından HttpTrigger parçası işlenir ve mekanizması Web kancası türüne göre değişir. Her mekanizması yok, ancak bir anahtar kullanır. Varsayılan olarak, "varsayılan" adlı işlevi anahtar kullanılır. Farklı bir anahtarı kullanmak istiyorsanız, aşağıdaki yollardan biriyle istek anahtarı adıyla göndermek için Web kancası sağlayıcısı yapılandırmanız gerekir:

- **Sorgu dizesi**: anahtar adına Sağlayıcının geçirdiği `clientid` sorgu dizesi parametresi (örneğin, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **İstek üst bilgisi**: anahtar adına Sağlayıcının geçirdiği `x-functions-clientid` üstbilgi.

> [!NOTE]
> İşlev tuşları, ana bilgisayar anahtarları önceliklidir. Aynı ada sahip iki anahtar tanımlanmışsa işlevi anahtar kullanılır.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>HTTP tetikleyicisi örnekleri
Aşağıdaki HTTP tetikleyicisini olduğunu varsayalım `bindings` function.json dizisi:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Arar dile özgü örnek bkz bir `name` parametresi sorgu dizesi veya HTTP istek gövdesi.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>HTTP tetikleyicisi örnek C# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

POCO yerine de bağlayabilirsiniz `HttpRequestMessage`. Bu JSON olarak ayrıştırılır, istek gövdesinden hydrated. Benzer şekilde, bir tür bağlama HTTP yanıt çıkışı geçirilebilir ve bu 200 durum koduyla yanıt gövdesi olarak döndürülür.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>F # HTTP tetikleyicisi örnek #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

Gereksinim duyduğunuz bir `project.json` NuGet başvurmak için kullanılan dosya `FSharp.Interop.Dynamic` ve `Dynamitey` derlemeler şuna benzer:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Bu NuGet bağımlılıklarınızı getirilemedi kullanacak ve bunları komut dosyanıza başvurur.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Node.JS HTTP tetikleyicisi örnek
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Web kancası örnekleri
Aşağıdaki Web kancası tetikleyici olduğunu varsayalım `bindings` function.json dizisi:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

GitHub sorunu yorum günlükleri dile özgü örneğe bakın.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Web kancası örnek C# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Web kancası örnek F # #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Node.JS Web kancası örnek
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

