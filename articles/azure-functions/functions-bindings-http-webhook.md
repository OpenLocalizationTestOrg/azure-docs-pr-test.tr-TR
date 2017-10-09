---
title: "aaaAzure işlevleri HTTP ve Web kancası bağlamaları | Microsoft Docs"
description: "Toouse HTTP ve Web kancası nasıl tetikler anlamak ve Azure işlevlerinde bağlar."
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
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Azure işlevleri HTTP ve Web kancası bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makale, tooconfigure ve iş HTTP ile nasıl tetikler açıklar ve Azure işlevlerinde bağlar.
Bu, Azure işlevleri toobuild sunucusuz API'ler ve yanıt toowebhooks kullanabilirsiniz.

Azure işlevleri bağlamaları aşağıdaki hello sağlar:
- Bir [HTTP tetikleyicisini](#httptrigger) bir HTTP isteğiyle bir işlevi çağırmak olanak tanır. Bu özelleştirilmiş toorespond çok olabilir[kancalarını](#hooktrigger).
- Bir [HTTP bağlama çıktı](#output) toorespond toohello istek sağlar.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>HTTP tetikleyicisi
Merhaba HTTP tetikleyicisini işlevinizin yanıt tooan HTTP istek yürütülür. Toorespond tooa belirli URL veya HTTP yöntemleri kümesini özelleştirebilirsiniz. Bir HTTP tetikleyicisi yapılandırılmış toorespond toowebhooks de olabilir. 

Hello işlevleri portalı kullanıyorsanız, aynı zamanda hemen önceden yapılmış bir şablon kullanarak başlayabiliriz. Seçin **yeni işlev** ve "API & Web Kancalarını" Merhaba **senaryo** açılır. Merhaba şablonlardan birini seçin ve tıklatın **oluşturma**.

Varsayılan olarak, bir HTTP tetikleyicisi toohello isteği bir HTTP 200 Tamam durum kodu ve boş bir gövde ile yanıt verir. toomodify Merhaba yanıt, yapılandırma bir [HTTP çıktı bağlama](#output)

### <a name="configuring-an-http-trigger"></a>Bir HTTP tetikleyicisi yapılandırma
Bir HTTP tetikleyicisi hello aşağıdaki JSON nesnesi benzer bir toohello de dahil olmak üzere tarafından tanımlanan `bindings` function.json dizisi:

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
Merhaba bağlama aşağıdaki özelliklere hello destekler:

* **ad** : gerekli - işlev kodu hello istek veya istek gövdesi için kullanılan hello değişken adı. Bkz: [bir HTTP tetikleyicisi koddan çalışan](#httptriggerusage).
* **tür** : gerekli - çok ayarlanmış olmalıdır "httpTrigger".
* **Yön** : gerekli - çok "içinde" ayarlanmış olmalıdır.
* _authLevel_ : Bu hangi anahtarları varsa, toobe sipariş tooinvoke hello işlevinde hello istekte mevcut gereksinim belirler. Bkz: [anahtarlarla çalışma](#keys) aşağıda. Merhaba değer hello aşağıdakilerden biri olabilir:
    * _Anonim_: Hayır API anahtarı gereklidir.
    * _işlev_: bir işleve özgü API anahtarı gereklidir. Hiçbiri sağlanmazsa hello varsayılan değer budur.
    * _Yönetici_ : hello ana anahtar gereklidir.
* **yöntemleri** : Bu toowhich hello işlevi yanıt hello HTTP yöntemleri dizisidir. Belirtilmezse, hello işlevi tooall HTTP yöntemleri yanıt verir. Bkz: [hello HTTP uç noktası özelleştirme](#url).
* **Rota** : Bu toowhich denetleme hello rota şablonu tanımlar işlevinizin yanıt URL'leri isteyin. Merhaba hiçbiri sağlanmazsa varsayılan değer: `<functionname>`. Bkz: [hello HTTP uç noktası özelleştirme](#url).
* **webHookType** : hello HTTP tetikleyicisi tooact bu hello belirtilen sağlayıcı için bir Web kancası reciever olarak yapılandırır. Merhaba _yöntemleri_ özelliği, değil Bu seçilirse ayarlanmalıdır. Bkz: [yanıt toowebhooks](#hooktrigger). Merhaba değer hello aşağıdakilerden biri olabilir:
    * _genericJson_ : belirli bir sağlayıcı için mantığı olmadan bir genel amaçlı Web kancası uç noktası.
    * _github_ : hello işlevi tooGitHub kancalarını yanıt verecektir. Merhaba _authLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.
    * _kayma_ : hello işlevi tooSlack kancalarını yanıt verecektir. Merhaba _authLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Bir HTTP tetikleyicisi kodu ile çalışma
C# ve F # işlevleri için tetikleyici giriş toobe hello türü ya da bildirebilirsiniz `HttpRequestMessage` veya özel bir tür. Seçerseniz `HttpRequestMessage`, tam erişim toohello istek nesnesi alırsınız. İçin özel bir tür (örneğin, bir POCO) işlevleri tooparse hello istek gövdesinde JSON toopopulate hello nesne özellikleri çalışacaktır.

Node.js işlevleri için hello işlevleri çalışma zamanı hello istek gövdesi yerine hello istek nesnesi sağlar.

Bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) örneğin kullanımları.


<a name="output"></a>
## <a name="http-response-output-binding"></a>HTTP yanıtının çıkış bağlama
Merhaba HTTP çıkış bağlama toorespond toohello HTTP isteği gönderen kullanın. Bu bağlamanın bir HTTP tetikleyicisi gerektirir ve hello tetikleyicinin istekle ilişkili toocustomize hello yanıt verir. Bir HTTP bağlaması çıktı bir HTTP tetikleyicisi boş bir gövde ile HTTP 200 Tamam döndürmeyecektir sağlanan olur. 

### <a name="configuring-an-http-output-binding"></a>Bir HTTP yapılandırma bağlama çıktı
Merhaba HTTP çıktı bağlama hello aşağıdaki JSON nesnesi benzer bir toohello dahil ederek tanımlanmış `bindings` function.json dizisi:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
Merhaba bağlama hello aşağıdaki özellikleri içerir:

* **ad** : hello yanıtı işlevi kod içinde kullanılan değişken adı gerekli - hello. Bkz: [bir HTTP ile çalışma çıktı kodundan bağlama](#outputusage).
* **tür** : gerekli - çok ayarlanmış olmalıdır "http".
* **Yön** : gerekli - çok "out" ayarlanmış olmalıdır.

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Bir HTTP ile çalışma kodundan bağlama çıktı
Http veya Web kancası hello çıkış parametresi (örneğin, "res") toorespond toohello arayan kullanabilirsiniz. Alternatif olarak, standart kullanabilirsiniz `Request.CreateResponse()` (C#) veya `context.res` (Node.JS) deseni tooreturn yanıt. Nasıl toouse hello ikinci yöntemi ile ilgili örnekler için bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) ve [Web kancası tetikleyici örnekleri](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Toowebhooks yanıt
Bir HTTP tetikleyicisi hello ile _webHookType_ özelliği olacaktır yapılandırılmış toorespond çok[kancalarını](https://en.wikipedia.org/wiki/Webhook). Merhaba temel yapılandırma hello "genericJson" ayarını kullanır. İstekleri tooonly olanlar HTTP POST ve hello kullanarak bu sınırlar `application/json` içerik türü.

Merhaba tetikleyici ayrıca uyarlanmış tooa belirli Web kancası sağlayıcı olabilir (örneğin, [GitHub](https://developer.github.com/webhooks/) ve [Slack'e](https://api.slack.com/outgoing-webhooks)). Bir sağlayıcı belirtilmemişse hello işlevleri çalışma zamanı hello sağlayıcının doğrulama mantığını sizin için dikkatli olun.  

### <a name="configuring-github-as-a-webhook-provider"></a>GitHub Web kancası sağlayıcısı olarak yapılandırma
toorespond tooGitHub kancalarını, önce bir HTTP tetikleyicisi ile işlevinizi oluşturun ve ayarlayın hello _webHookType_ özelliği çok "github". Ardından kopyalama kendi [URL](#url) ve [API anahtarı](#keys) GitHub deponun içine **Web kancası eklemek** sayfası. GitHub'ınızın bkz [Web kancası oluşturma](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) daha fazla bilgi için belgeleri.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Bir Web kancası sağlayıcısı olarak kayma yapılandırma
Merhaba Slack Web kancası işlevi özel bir anahtar kayma hello belirtecinden ile yapılandırmanız gerekir, belirtmenize izin verir yerine bir belirteç sizin için oluşturur. Bkz: [anahtarlarla çalışma](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Merhaba HTTP uç noktası özelleştirme
Bir HTTP tetikleyicisi ya da Web kancası, bir işlev oluşturduğunuzda varsayılan olarak hello işlevi adreslenebilir hello formunun bir yol şu şekildedir:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

İsteğe bağlı hello kullanarak bu yolun özelleştirebilirsiniz `route` hello HTTP tetikleyicisi özellikte bağlama girdisini. Aşağıdaki örnek olarak, hello *function.json* dosya tanımlayan bir `route` özelliği bir HTTP tetikleyicisi için:

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

Bu yapılandırma, hello işlevi artık rota hello özgün yol yerine aşağıdaki hello ile adreslenebilir kullanmaktır.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Bu, toosupport iki parametrelerinde hello adresi, "kategorisi" ve "id" Merhaba işlev kodu sağlar. Kullanabilirsiniz [Web API rota kısıtlaması](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) , parametrelere sahip. C# işlev kodu aşağıdaki Merhaba parametrelerinin her ikisini de kullanır.

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

Aynı yol parametreleri Node.js işlevi kod toouse hello aşağıdadır.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

Varsayılan olarak, tüm işlevi yollar ile önek *API*. Ayrıca özelleştirme veya hello kullanan hello öneki kaldırın `http.routePrefix` özelliğinde, *host.json* dosya. Merhaba aşağıdaki örnek kaldırır hello *API* hello hello önekini için boş bir dize kullanarak rota öneki *host.json* dosya.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Hakkında ayrıntılı bilgi için tooupdate hello *host.json* bakın, işlevinizi dosyası [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate). 

Diğer özellikler hakkında bilgi için yapılandırabileceğiniz, *host.json* dosya için bkz: [host.json başvuru](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Anahtarları ile çalışma
HttpTriggers ek güvenlik için anahtarları yararlanabilirsiniz. Standart HttpTrigger hello anahtar toobe hello istekte mevcut gerektiren bir API anahtarı olarak kullanabilirsiniz. Web kancası anahtarları tooauthorize isteklerini bir hangi hello sağlayıcının desteklediği bağlı olarak, çeşitli şekillerde kullanabilirsiniz.

Anahtarları azure'da işlevi uygulamanız bir parçası olarak depolanır ve bekleyen şifrelenir. tooview, anahtarlarınızı yenilerini oluşturun veya toplama anahtarları toonew değerleri, işlevlerinizi hello portalındaki tooone gidin ve "Manage" seçin 

Anahtarların iki tür vardır:
- **Ana bilgisayar anahtarları**: Bu anahtarları hello işlevi uygulamasında tüm işlevleri tarafından paylaşılır. Bir API anahtarı olarak kullanıldığında, bunlar erişim tooany işlevi hello işlevi uygulama içinde izin verir.
- **İşlev tuşları**: Bu anahtarların bunlar tanımlanan yalnızca toohello belirli işlevler Uygula. Bunlar yalnızca, bir API anahtarı olarak kullanıldığında, erişim toothat işlevi sağlar.

Her anahtar için başvuru olarak adlandırılır ve hello işlevi ve ana bilgisayar düzeyinde ("varsayılan" adlı) bir varsayılan anahtar yok. Merhaba **ana anahtar** varsayılan ana bilgisayar anahtarı "her işlev uygulaması için tanımlanır ve iptal edilemiyor _master" olarak adlandırılmıştır. Yönetim erişimi toohello çalışma zamanı API'ler sağlar. Kullanarak `"authLevel": "admin"` hello JSON bağlama hello istek üzerine sunulan bu anahtar toobe gerekir; başka bir anahtar bir yetkilendirme hatasına neden olur.

> [!NOTE]
> Son toohello yükseltilmiş hello ana anahtar ile bu anahtarı üçüncü taraflarla paylaşma veya gerekir yerel istemci uygulamalarında dağıtmak izinler. Hello Yöneticisi yetki düzeyini seçerken dikkatli olun.
> 
> 

### <a name="api-key-authorization"></a>API anahtarı yetkilendirme
Varsayılan olarak, bir HttpTrigger hello HTTP isteği bir API anahtarı gerektirir. Bu nedenle, HTTP isteği normalde şöyle görünür:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

Merhaba anahtar adlı bir sorgu dizesi değişkeni dahil edilebilir `code`, yukarıdaki olarak veya içinde eklenebilir bir `x-functions-key` HTTP üstbilgisi. Merhaba hello anahtarının değerini hello işlev için tanımlanmış herhangi bir işlev tuşu veya tüm ana bilgisayar anahtarı olabilir.

Anahtarları olmadan tooallow isteklerin seçin veya bu hello ana anahtar hello değiştirerek kullanılmalıdır belirtin `authLevel` JSON bağlama hello özelliğinde (bkz [HTTP tetikleyicisini](#httptrigger)).

### <a name="keys-and-webhooks"></a>Anahtarlar ve Web kancaları
Web kancası yetkilendirme hello Web kancası reciever bileşeni tarafından yapılır, hello HttpTrigger ve hello mekanizması parçası hello Web kancası türüne göre değişir. Her mekanizması yok, ancak bir anahtar kullanır. Varsayılan olarak, "varsayılan" adlı hello işlevi anahtar kullanılır. Farklı bir anahtar toouse isterseniz tooconfigure hello Web kancası sağlayıcı toosend hello anahtar adı hello istek yolu izleyerek hello birinde ile gerekir:

- **Sorgu dizesi**: hello sağlayıcısı hello hello anahtar adı geçen `clientid` sorgu dizesi parametresi (örneğin, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **İstek üst bilgisi**: hello sağlayıcısı hello hello anahtar adı geçen `x-functions-clientid` üstbilgi.

> [!NOTE]
> İşlev tuşları, ana bilgisayar anahtarları önceliklidir. İki anahtar ile aynı adı, hello hello tanımlanmışsa, işlev tuşu kullanılır.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>HTTP tetikleyicisi örnekleri
Merhaba, HTTP tetikleyicisini aşağıdaki hello olduğunu varsayalım `bindings` function.json dizisi:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Arar hello dile özgü örnek bkz bir `name` parametresi hello sorgu dizesi veya hello hello HTTP istek gövdesi.

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

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

Tooa POCO de bağlayabilirsiniz yerine `HttpRequestMessage`. Bu hello isteği, JSON olarak ayrıştırılır hello gövdesi gelen hydrated. Benzer şekilde, bir tür bağlama toohello HTTP yanıt çıktısı geçirilebilir ve bu 200 durum koduyla hello yanıt gövdesi olarak döndürülür.
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

Gereksinim duyduğunuz bir `project.json` NuGet tooreference hello kullanan bir dosyayı `FSharp.Interop.Dynamic` ve `Dynamitey` derlemeler şuna benzer:

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

Bu, NuGet toofetch bağımlılıklarınızı kullanacak ve bunları komut dosyanıza başvurur.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Node.JS HTTP tetikleyicisi örnek
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Web kancası örnekleri
Web kancası tetikleyici hello aşağıdaki hello olduğunu varsayalım `bindings` function.json dizisi:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

GitHub sorunu yorum günlükleri hello dile özgü örneğine bakın.

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

