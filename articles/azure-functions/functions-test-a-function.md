---
title: "Azure işlevleri aaaTesting | Microsoft Docs"
description: "Postman, cURL ve Node.js kullanarak Azure işlevlerinizi test edin."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme, Web kancalarını, dinamik işlem, sunucusuz mimari, test etme"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Azure işlevleri, kodunuzu test etmek için stratejileri

Bu konu genel aşağıdaki hello kullanımı dahil olmak üzere çeşitli yolları tootest işlevleri yaklaşıyor hello gösterir:

+ CURL, Postman ve web tabanlı tetikleyiciler için bile bir web tarayıcısı gibi HTTP tabanlı araçları
+ Azure Storage Gezgini, tootest Azure depolama tabanlı Tetikleyicileri
+ Hello Azure işlevleri portalındaki test sekmesi
+ Zamanlayıcı tarafından tetiklenen işlevi
+ Uygulama veya framework test etme

Tüm bu yöntemleri sınama ya da girişini kabul eden bir HTTP tetikleyicisi işlevi bir sorgu dizesi parametresi veya hello istek gövdesi kullanın. Bu işlev hello ilk bölümünde oluşturabilirsiniz.

## <a name="create-a-function-for-testing"></a>Test etmek için bir işlev oluşturun
Bu öğretici çoğu için hello HttpTrigger JavaScript işlevi, bir işlev oluşturduğunuzda kullanılabilir olan bir şablon biraz değiştirilmiş bir sürümünü kullanın. Bir işlev oluşturma yardıma gereksinim duyarsanız, bu gözden [Öğreticisi](functions-create-first-azure-function.md). Merhaba seçin **HttpTrigger - JavaScript** hello test işlevi hello oluştururken şablonu [Azure portal].

Merhaba varsayılan işlevi temelde hello istek gövdesi veya sorgu dizesi parametresi, geri hello adından görüntülemektedir "hello world" işlevi şablonudur `name=<your name>`.  Biz hello kod güncelleştireceğim tooalso izin tooprovide hello adı ve adresi hello istek gövdesinde JSON içeriği olarak. Ardından hello işlevi kullanılabilir olduğunda bu geri toohello istemci görüntülemektedir.   

Merhaba işlevi hello test etmek için kullanacağız kodu aşağıdaki ile güncelleştirin:

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>Test araçları ile işlevi
Hello Azure portal dışında tootrigger işlevlerinizi test etmek için kullanabileceğiniz çeşitli araçlar vardır. Bu araçlar (hem kullanıcı Arabirimi tabanlı ve komut satırı), Azure depolama erişim araçları ve basit bir web tarayıcısı test HTTP içerir.

### <a name="test-with-a-browser"></a>Bir tarayıcı ile test
HTTP üzerinden basit yol tootrigger işlevleri Hello web tarayıcısıdır. Gövde yükü gerektirmeyen GET istekleri için bir tarayıcı kullanabilir ve kullanım yalnızca sorgu parametreleri dize.

daha önce tanımladığımız, kopya hello tootest hello işlevi **işlevi Url** hello portalından. Form aşağıdaki hello sahiptir:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Merhaba append `name` parametre toohello sorgu dizesi. Hello için gerçek bir ad kullanmak `<Enter a name here>` yer tutucu.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

Tarayıcınız ve Yapıştır hello URL'ye yanıt benzer toohello aşağıdaki almanız gerekir.

![Test yanıt ekran görüntüsü, Chrome tarayıcı sekmesi](./media/functions-test-a-function/browser-test.png)

XML dizesi döndürdü hello sarmalar hello Chrome tarayıcısı örnektir. Diğer tarayıcılarda yalnızca hello dize değeri görüntüler.

Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Postman ile test
Aracı tootest önerilen hello işlevlerinizi çoğunu hello Chrome tarayıcı ile tümleşir Postman değil. tooinstall Postman, bkz: [almak Postman](https://www.getpostman.com/). Postman pek çok daha fazla öznitelik bir HTTP isteği üzerinde denetim sağlar.

> [!TIP]
> En çok rahat hello HTTP sınama aracını kullanın. Bazı alternatifleri tooPostman şunlardır:  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Pençe](https://luckymarmot.com/paw)  
>
>

Postman istek gövdesinde hello işleviyle tootest:

1. Postman hello Başlat **uygulamaları** bir Chrome tarayıcı penceresinde hello sol üst köşesindeki düğmesi.
2. Kopyalama, **işlevi Url**, Postman yapıştırın. Merhaba erişim kodu sorgu dizesi parametresi içerir.
3. Merhaba HTTP yöntemini çok değiştirme**POST**.
4. Tıklatın **gövde** > **ham**ve JSON istek gövdesi benzer toohello aşağıdakileri ekleyin:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Tıklatın **Gönder**.

Merhaba aşağıdaki görüntüde test hello basit Yankı işlevi örnek Bu öğreticide gösterir.

![Ekran görüntüsü, Postman kullanıcı arabirimi](./media/functions-test-a-function/postman-test.png)

Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>CURL hello komut satırından test
Genellikle, yazılım test ederken, gerekli toolook her komut satırı toohelp debug uygulamanızı hello daha fazla değil. Bu işlevler testi ile farklı değildir. Merhaba cURL Linux tabanlı sistemlerinde varsayılan olarak kullanılabilir olduğunu unutmayın. Windows, öncelikle hello yükleyip [cURL aracı](https://curl.haxx.se/).

daha önce kopyalama hello tanımladığımız tootest hello işlevi **işlevi URL** hello portalından. Form aşağıdaki hello sahiptir:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Bu hello işlevinizi tetiklemek için URL'dir. Bu hello komut satırı toomake üzerinde hello cURL komutunu kullanarak bir GET test (`-G` veya `--get`) hello işlevi karşı isteği:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Bu belirli örnek verileri olarak geçirilen bir sorgu dizesi parametresi gerektirir (`-d`) komutu hello cURL:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Çalışma hello komut ve çıktı hello işlevinin hello komut satırında aşağıdaki hello bakın:

![Komut istemi ekran çıktı](./media/functions-test-a-function/curl-test.png)

Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Depolama Gezgini'ni kullanarak bir blob tetikleyici test
Bir blob Tetik işlevi kullanarak test edebilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/).

1. Merhaba, [Azure portal] işlevi uygulamanız için bir C#, F # veya JavaScript blob tetikleyici işlev oluşturun. Merhaba yol toomonitor toohello blob kapsayıcı adını ayarlayın. Örneğin:

        files
2. Merhaba tıklatın  **+**  düğmesini tooselect veya toouse istediğiniz hello depolama hesabı oluşturun. Sonra **Oluştur**’a tıklayın.
3. Metin aşağıdaki hello ile bir metin dosyası oluşturun ve kaydedin:

        A text file for blob trigger function testing.
4. Çalıştırma [Azure Storage Gezgini](http://storageexplorer.com/)ve toohello blob kapsayıcısında izlenmekte olan hello depolama hesabı bağlayın.
5. Tıklatın **karşıya** tooupload hello metin dosyası.

    ![Depolama Gezgini ekran görüntüsü](./media/functions-test-a-function/azure-storage-explorer-test.png)

Merhaba varsayılan blob Tetik işlevi kodu hello blob hello günlüklerine hello işlenmesini raporları:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>İşlevler içinde işlevi test etme
Hello Azure işlevleri portalına tasarlanmıştır HTTP ve Zamanlayıcı test toolet tetiklenen işlevleri. Test ettiğiniz diğer işlevleri işlevleri tootrigger de oluşturabilirsiniz.

### <a name="test-with-hello-functions-portal-run-button"></a>Merhaba işlevleri portal Çalıştır düğmesi ile test
Merhaba portal sağlar bir **çalıştırmak** toodo bazı kullanabileceğiniz düğmesi sınırlı test etme. Merhaba düğmesini kullanarak bir istek gövdesi sağlayabilirsiniz, ancak sorgu dizesi parametreleri belirtin veya istek üstbilgileri güncelleştirin.

Test oluşturduğumuz önceki hello aşağıdaki JSON dizesi benzer bir toohello ekleyerek hello HTTP tetikleyicisi işlevi **istek gövdesinde** alan. Merhaba ardından **çalıştırmak** düğmesi.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Zamanlayıcı tetikleyicisi ile test
Bazı işlevler yeterli daha önce bahsedilen hello araçlarıyla sınanamıyor. Örneğin, bir ileti içine bırakıldığında çalıştırılan bir sıra tetikleyici işlevi göz önünde bulundurun [Azure kuyruk depolama](../storage/queues/storage-dotnet-how-to-use-queues.md). Her zaman kodu toodrop bir ileti, sıraya yazabilir, ve bunun bir örneğini konsol projesinde bu makalenin sonraki bölümlerinde sağlanır. Ancak, işlevleri doğrudan test kullanabileceğiniz başka bir yaklaşım yoktur.  

Bir sıra ile yapılandırılmış bir süreölçer tetikleyici kullanabilirsiniz bağlama çıktı. Bu zamanlayıcı tetikleyicisi kod sonra hello sınama iletileri toohello sırası yazabilirsiniz. Bu bölüm bir örnek anlatılmaktadır.

Hello Azure işlevleriyle bağlamaları kullanma hakkında daha ayrıntılı bilgi için bkz: [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Test etmek için bir sıra Tetikleyici oluşturma
toodemonstrate bu yaklaşım ilk adlı bir kuyruk için tootest istiyoruz bir sıra Tetik işlevi oluşturuyoruz `queue-newusers`. Bu işlev, yeni bir kullanıcı için kuyruk depolama alanına bırakılan ad ve adres bilgilerini işler.

> [!NOTE]
> Farklı sıra adı kullanırsanız, kullandığınız hello ad uyumlu toohello emin olun [adlandırma kuyrukları ve meta verileri](https://msdn.microsoft.com/library/dd179349.aspx) kuralları. Aksi takdirde bir hata alıyorsunuz.
>
>

1. Merhaba, [Azure portal] işlev uygulamanız için tıklatın **yeni işlev** > **QueueTrigger - C#**.
2. Merhaba sıra işlevi tarafından izlenen hello kuyruk adı toobe girin:

        queue-newusers
3. Merhaba tıklatın  **+**  düğmesini tooselect veya toouse istediğiniz hello depolama hesabı oluşturun. Sonra **Oluştur**’a tıklayın.
4. Merhaba varsayılan sıra işlevi şablon kodu hello günlük girişlerini izleyebilmek bu portal tarayıcı penceresini açık bırakın.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Bir zamanlayıcı tetikleyicisi toodrop bir ileti hello kuyruk oluşturma
1. Açık hello [Azure portal] yeni bir tarayıcı penceresinde ve tooyour işlevi uygulamasına gidin.
2. Tıklatın **yeni işlev** > **TimerTrigger - C#**. Cron ifade tooset girin ne sıklıkta hello Zamanlayıcı kod sıra işlevinizi test eder. Sonra **Oluştur**’a tıklayın. Her 30 saniyede hello test toorun istiyorsanız hello aşağıdakileri kullanabilirsiniz [CRON ifade](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Merhaba tıklatın **tümleştir** yeni Zamanlayıcı tetikleyicinizin sekmesi.
4. Altında **çıkış**, tıklatın **+ yeni çıktı**. Ardından **sıra** ve **seçin**.
5. Merhaba kullandığınız not hello ad **sıraya ileti nesnesi**. Merhaba Zamanlayıcı işlev kodu kullanabilirsiniz.

        myQueue
6. Burada selamlama iletisine gönderilen Hello sıra adı girin:

        queue-newusers
7. Merhaba tıklatın  **+**  düğmesini kullandığınız önceden hello sıra tetikleyiciyle tooselect hello depolama hesabı. Daha sonra **Kaydet**'e tıklayın.
8. Merhaba tıklatın **geliştirme** Zamanlayıcı tetikleyicinizin sekmesi.
9. İleti nesne adı daha önce gösterilen aynı sıraya hello kullanılan sürece hello C# Zamanlayıcı işlevi için koddan hello kullanabilirsiniz. Daha sonra **Kaydet**'e tıklayın.

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

Bu noktada, hello örnek cron ifade kullandıysanız hello C# Zamanlayıcı işlevi her 30 saniyede yürütür. Merhaba günlükleri hello Zamanlayıcı işlevi için her yürütme raporu:

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

Merhaba tarayıcı penceresinde hello sıra işlevi için işlenmekte olan her bir ileti görebilirsiniz:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Kod ile işlevi test etme
İşlevlerinizi toocreate dış bir uygulama veya framework tootest gerekebilir.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Bir HTTP tetikleyicisi işlevini koduyla test: Node.js
Bir Node.js uygulaması tooexecute bir HTTP isteği tootest işlevinizi kullanabilirsiniz.
Tooset emin olun:

* Merhaba `host` hello isteği seçenekleri tooyour işlevi uygulama konaktaki.
* Merhaba, işlev adı `path`.
* Erişim kodunuzu (`<your code>`) hello içinde `path`.

Kod örneği:

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


Çıktı:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Bir kuyruk tetikleyici işlevini koduyla test: C# #
Kuyrukta kod toodrop bir ileti kullanarak bir sıra tetikleyici test edebilirsiniz daha önce bahsedilen. Aşağıdaki kod örneği hello hello sunulan hello C# kod temel [Azure kuyruk depolamaya başlama](../storage/queues/storage-dotnet-how-to-use-queues.md) Öğreticisi. Kod diğer diller için de bu bağlantıdan bulunmaktadır.

tootest bu kodu bir konsol uygulamasında yapmanız gerekir:

* [Merhaba app.config dosyasında depolama bağlantı dizelerinizi yapılandırma](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Geçirmek bir `name` ve `address` parametreleri toohello uygulama olarak. Örneğin, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Bu kodu hello ad ve adres yeni bir kullanıcı için komut satırı bağımsız değişkenleri olarak çalışma zamanı sırasında kabul eder.)

Örnek C# kod:

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

Merhaba tarayıcı penceresinde hello sıra işlevi için işlenmekte olan her bir ileti görebilirsiniz:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure portal]: https://portal.azure.com
