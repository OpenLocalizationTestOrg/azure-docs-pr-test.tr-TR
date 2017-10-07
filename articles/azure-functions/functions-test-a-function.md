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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="0e73f-104">Azure işlevleri, kodunuzu test etmek için stratejileri</span><span class="sxs-lookup"><span data-stu-id="0e73f-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="0e73f-105">Bu konu genel aşağıdaki hello kullanımı dahil olmak üzere çeşitli yolları tootest işlevleri yaklaşıyor hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="0e73f-106">CURL, Postman ve web tabanlı tetikleyiciler için bile bir web tarayıcısı gibi HTTP tabanlı araçları</span><span class="sxs-lookup"><span data-stu-id="0e73f-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="0e73f-107">Azure Storage Gezgini, tootest Azure depolama tabanlı Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="0e73f-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="0e73f-108">Hello Azure işlevleri portalındaki test sekmesi</span><span class="sxs-lookup"><span data-stu-id="0e73f-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="0e73f-109">Zamanlayıcı tarafından tetiklenen işlevi</span><span class="sxs-lookup"><span data-stu-id="0e73f-109">Timer-triggered function</span></span>
+ <span data-ttu-id="0e73f-110">Uygulama veya framework test etme</span><span class="sxs-lookup"><span data-stu-id="0e73f-110">Testing application or framework</span></span>

<span data-ttu-id="0e73f-111">Tüm bu yöntemleri sınama ya da girişini kabul eden bir HTTP tetikleyicisi işlevi bir sorgu dizesi parametresi veya hello istek gövdesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="0e73f-112">Bu işlev hello ilk bölümünde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e73f-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="0e73f-113">Test etmek için bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="0e73f-113">Create a function for testing</span></span>
<span data-ttu-id="0e73f-114">Bu öğretici çoğu için hello HttpTrigger JavaScript işlevi, bir işlev oluşturduğunuzda kullanılabilir olan bir şablon biraz değiştirilmiş bir sürümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="0e73f-115">Bir işlev oluşturma yardıma gereksinim duyarsanız, bu gözden [Öğreticisi](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="0e73f-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="0e73f-116">Merhaba seçin **HttpTrigger - JavaScript** hello test işlevi hello oluştururken şablonu [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0e73f-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="0e73f-117">Merhaba varsayılan işlevi temelde hello istek gövdesi veya sorgu dizesi parametresi, geri hello adından görüntülemektedir "hello world" işlevi şablonudur `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="0e73f-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="0e73f-118">Biz hello kod güncelleştireceğim tooalso izin tooprovide hello adı ve adresi hello istek gövdesinde JSON içeriği olarak.</span><span class="sxs-lookup"><span data-stu-id="0e73f-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="0e73f-119">Ardından hello işlevi kullanılabilir olduğunda bu geri toohello istemci görüntülemektedir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="0e73f-120">Merhaba işlevi hello test etmek için kullanacağız kodu aşağıdaki ile güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="0e73f-120">Update hello function with hello following code, which we will use for testing:</span></span>

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

## <a name="test-a-function-with-tools"></a><span data-ttu-id="0e73f-121">Test araçları ile işlevi</span><span class="sxs-lookup"><span data-stu-id="0e73f-121">Test a function with tools</span></span>
<span data-ttu-id="0e73f-122">Hello Azure portal dışında tootrigger işlevlerinizi test etmek için kullanabileceğiniz çeşitli araçlar vardır.</span><span class="sxs-lookup"><span data-stu-id="0e73f-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="0e73f-123">Bu araçlar (hem kullanıcı Arabirimi tabanlı ve komut satırı), Azure depolama erişim araçları ve basit bir web tarayıcısı test HTTP içerir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="0e73f-124">Bir tarayıcı ile test</span><span class="sxs-lookup"><span data-stu-id="0e73f-124">Test with a browser</span></span>
<span data-ttu-id="0e73f-125">HTTP üzerinden basit yol tootrigger işlevleri Hello web tarayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="0e73f-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="0e73f-126">Gövde yükü gerektirmeyen GET istekleri için bir tarayıcı kullanabilir ve kullanım yalnızca sorgu parametreleri dize.</span><span class="sxs-lookup"><span data-stu-id="0e73f-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="0e73f-127">daha önce tanımladığımız, kopya hello tootest hello işlevi **işlevi Url** hello portalından.</span><span class="sxs-lookup"><span data-stu-id="0e73f-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="0e73f-128">Form aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="0e73f-129">Merhaba append `name` parametre toohello sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="0e73f-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="0e73f-130">Hello için gerçek bir ad kullanmak `<Enter a name here>` yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="0e73f-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="0e73f-131">Tarayıcınız ve Yapıştır hello URL'ye yanıt benzer toohello aşağıdaki almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Test yanıt ekran görüntüsü, Chrome tarayıcı sekmesi](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="0e73f-133">XML dizesi döndürdü hello sarmalar hello Chrome tarayıcısı örnektir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="0e73f-134">Diğer tarayıcılarda yalnızca hello dize değeri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0e73f-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="0e73f-135">Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="0e73f-136">Postman ile test</span><span class="sxs-lookup"><span data-stu-id="0e73f-136">Test with Postman</span></span>
<span data-ttu-id="0e73f-137">Aracı tootest önerilen hello işlevlerinizi çoğunu hello Chrome tarayıcı ile tümleşir Postman değil.</span><span class="sxs-lookup"><span data-stu-id="0e73f-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="0e73f-138">tooinstall Postman, bkz: [almak Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="0e73f-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="0e73f-139">Postman pek çok daha fazla öznitelik bir HTTP isteği üzerinde denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e73f-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="0e73f-140">En çok rahat hello HTTP sınama aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="0e73f-141">Bazı alternatifleri tooPostman şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0e73f-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="0e73f-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="0e73f-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="0e73f-143">Pençe</span><span class="sxs-lookup"><span data-stu-id="0e73f-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="0e73f-144">Postman istek gövdesinde hello işleviyle tootest:</span><span class="sxs-lookup"><span data-stu-id="0e73f-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="0e73f-145">Postman hello Başlat **uygulamaları** bir Chrome tarayıcı penceresinde hello sol üst köşesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e73f-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="0e73f-146">Kopyalama, **işlevi Url**, Postman yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="0e73f-147">Merhaba erişim kodu sorgu dizesi parametresi içerir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="0e73f-148">Merhaba HTTP yöntemini çok değiştirme**POST**.</span><span class="sxs-lookup"><span data-stu-id="0e73f-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="0e73f-149">Tıklatın **gövde** > **ham**ve JSON istek gövdesi benzer toohello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e73f-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="0e73f-150">Tıklatın **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="0e73f-150">Click **Send**.</span></span>

<span data-ttu-id="0e73f-151">Merhaba aşağıdaki görüntüde test hello basit Yankı işlevi örnek Bu öğreticide gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Ekran görüntüsü, Postman kullanıcı arabirimi](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="0e73f-153">Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="0e73f-154">CURL hello komut satırından test</span><span class="sxs-lookup"><span data-stu-id="0e73f-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="0e73f-155">Genellikle, yazılım test ederken, gerekli toolook her komut satırı toohelp debug uygulamanızı hello daha fazla değil.</span><span class="sxs-lookup"><span data-stu-id="0e73f-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="0e73f-156">Bu işlevler testi ile farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-156">This is no different with testing functions.</span></span> <span data-ttu-id="0e73f-157">Merhaba cURL Linux tabanlı sistemlerinde varsayılan olarak kullanılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="0e73f-158">Windows, öncelikle hello yükleyip [cURL aracı](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="0e73f-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="0e73f-159">daha önce kopyalama hello tanımladığımız tootest hello işlevi **işlevi URL** hello portalından.</span><span class="sxs-lookup"><span data-stu-id="0e73f-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="0e73f-160">Form aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="0e73f-161">Bu hello işlevinizi tetiklemek için URL'dir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="0e73f-162">Bu hello komut satırı toomake üzerinde hello cURL komutunu kullanarak bir GET test (`-G` veya `--get`) hello işlevi karşı isteği:</span><span class="sxs-lookup"><span data-stu-id="0e73f-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="0e73f-163">Bu belirli örnek verileri olarak geçirilen bir sorgu dizesi parametresi gerektirir (`-d`) komutu hello cURL:</span><span class="sxs-lookup"><span data-stu-id="0e73f-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="0e73f-164">Çalışma hello komut ve çıktı hello işlevinin hello komut satırında aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0e73f-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Komut istemi ekran çıktı](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="0e73f-166">Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="0e73f-167">Depolama Gezgini'ni kullanarak bir blob tetikleyici test</span><span class="sxs-lookup"><span data-stu-id="0e73f-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="0e73f-168">Bir blob Tetik işlevi kullanarak test edebilirsiniz [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0e73f-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="0e73f-169">Merhaba, [Azure portal] işlevi uygulamanız için bir C#, F # veya JavaScript blob tetikleyici işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e73f-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="0e73f-170">Merhaba yol toomonitor toohello blob kapsayıcı adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="0e73f-171">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0e73f-171">For example:</span></span>

        files
2. <span data-ttu-id="0e73f-172">Merhaba tıklatın  **+**  düğmesini tooselect veya toouse istediğiniz hello depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e73f-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="0e73f-173">Sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-173">Then click **Create**.</span></span>
3. <span data-ttu-id="0e73f-174">Metin aşağıdaki hello ile bir metin dosyası oluşturun ve kaydedin:</span><span class="sxs-lookup"><span data-stu-id="0e73f-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="0e73f-175">Çalıştırma [Azure Storage Gezgini](http://storageexplorer.com/)ve toohello blob kapsayıcısında izlenmekte olan hello depolama hesabı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="0e73f-176">Tıklatın **karşıya** tooupload hello metin dosyası.</span><span class="sxs-lookup"><span data-stu-id="0e73f-176">Click **Upload** tooupload hello text file.</span></span>

    ![Depolama Gezgini ekran görüntüsü](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="0e73f-178">Merhaba varsayılan blob Tetik işlevi kodu hello blob hello günlüklerine hello işlenmesini raporları:</span><span class="sxs-lookup"><span data-stu-id="0e73f-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="0e73f-179">İşlevler içinde işlevi test etme</span><span class="sxs-lookup"><span data-stu-id="0e73f-179">Test a function within functions</span></span>
<span data-ttu-id="0e73f-180">Hello Azure işlevleri portalına tasarlanmıştır HTTP ve Zamanlayıcı test toolet tetiklenen işlevleri.</span><span class="sxs-lookup"><span data-stu-id="0e73f-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="0e73f-181">Test ettiğiniz diğer işlevleri işlevleri tootrigger de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e73f-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="0e73f-182">Merhaba işlevleri portal Çalıştır düğmesi ile test</span><span class="sxs-lookup"><span data-stu-id="0e73f-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="0e73f-183">Merhaba portal sağlar bir **çalıştırmak** toodo bazı kullanabileceğiniz düğmesi sınırlı test etme.</span><span class="sxs-lookup"><span data-stu-id="0e73f-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="0e73f-184">Merhaba düğmesini kullanarak bir istek gövdesi sağlayabilirsiniz, ancak sorgu dizesi parametreleri belirtin veya istek üstbilgileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e73f-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="0e73f-185">Test oluşturduğumuz önceki hello aşağıdaki JSON dizesi benzer bir toohello ekleyerek hello HTTP tetikleyicisi işlevi **istek gövdesinde** alan.</span><span class="sxs-lookup"><span data-stu-id="0e73f-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="0e73f-186">Merhaba ardından **çalıştırmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e73f-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="0e73f-187">Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="0e73f-188">Zamanlayıcı tetikleyicisi ile test</span><span class="sxs-lookup"><span data-stu-id="0e73f-188">Test with a timer trigger</span></span>
<span data-ttu-id="0e73f-189">Bazı işlevler yeterli daha önce bahsedilen hello araçlarıyla sınanamıyor.</span><span class="sxs-lookup"><span data-stu-id="0e73f-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="0e73f-190">Örneğin, bir ileti içine bırakıldığında çalıştırılan bir sıra tetikleyici işlevi göz önünde bulundurun [Azure kuyruk depolama](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="0e73f-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="0e73f-191">Her zaman kodu toodrop bir ileti, sıraya yazabilir, ve bunun bir örneğini konsol projesinde bu makalenin sonraki bölümlerinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0e73f-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="0e73f-192">Ancak, işlevleri doğrudan test kullanabileceğiniz başka bir yaklaşım yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e73f-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="0e73f-193">Bir sıra ile yapılandırılmış bir süreölçer tetikleyici kullanabilirsiniz bağlama çıktı.</span><span class="sxs-lookup"><span data-stu-id="0e73f-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="0e73f-194">Bu zamanlayıcı tetikleyicisi kod sonra hello sınama iletileri toohello sırası yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e73f-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="0e73f-195">Bu bölüm bir örnek anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0e73f-195">This section walks through an example.</span></span>

<span data-ttu-id="0e73f-196">Hello Azure işlevleriyle bağlamaları kullanma hakkında daha ayrıntılı bilgi için bkz: [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0e73f-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="0e73f-197">Test etmek için bir sıra Tetikleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e73f-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="0e73f-198">toodemonstrate bu yaklaşım ilk adlı bir kuyruk için tootest istiyoruz bir sıra Tetik işlevi oluşturuyoruz `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="0e73f-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="0e73f-199">Bu işlev, yeni bir kullanıcı için kuyruk depolama alanına bırakılan ad ve adres bilgilerini işler.</span><span class="sxs-lookup"><span data-stu-id="0e73f-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="0e73f-200">Farklı sıra adı kullanırsanız, kullandığınız hello ad uyumlu toohello emin olun [adlandırma kuyrukları ve meta verileri](https://msdn.microsoft.com/library/dd179349.aspx) kuralları.</span><span class="sxs-lookup"><span data-stu-id="0e73f-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="0e73f-201">Aksi takdirde bir hata alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="0e73f-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="0e73f-202">Merhaba, [Azure portal] işlev uygulamanız için tıklatın **yeni işlev** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="0e73f-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="0e73f-203">Merhaba sıra işlevi tarafından izlenen hello kuyruk adı toobe girin:</span><span class="sxs-lookup"><span data-stu-id="0e73f-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="0e73f-204">Merhaba tıklatın  **+**  düğmesini tooselect veya toouse istediğiniz hello depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e73f-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="0e73f-205">Sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-205">Then click **Create**.</span></span>
4. <span data-ttu-id="0e73f-206">Merhaba varsayılan sıra işlevi şablon kodu hello günlük girişlerini izleyebilmek bu portal tarayıcı penceresini açık bırakın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="0e73f-207">Bir zamanlayıcı tetikleyicisi toodrop bir ileti hello kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e73f-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="0e73f-208">Açık hello [Azure portal] yeni bir tarayıcı penceresinde ve tooyour işlevi uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="0e73f-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="0e73f-209">Tıklatın **yeni işlev** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="0e73f-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="0e73f-210">Cron ifade tooset girin ne sıklıkta hello Zamanlayıcı kod sıra işlevinizi test eder.</span><span class="sxs-lookup"><span data-stu-id="0e73f-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="0e73f-211">Sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-211">Then click **Create**.</span></span> <span data-ttu-id="0e73f-212">Her 30 saniyede hello test toorun istiyorsanız hello aşağıdakileri kullanabilirsiniz [CRON ifade](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="0e73f-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="0e73f-213">Merhaba tıklatın **tümleştir** yeni Zamanlayıcı tetikleyicinizin sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0e73f-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="0e73f-214">Altında **çıkış**, tıklatın **+ yeni çıktı**.</span><span class="sxs-lookup"><span data-stu-id="0e73f-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="0e73f-215">Ardından **sıra** ve **seçin**.</span><span class="sxs-lookup"><span data-stu-id="0e73f-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="0e73f-216">Merhaba kullandığınız not hello ad **sıraya ileti nesnesi**.</span><span class="sxs-lookup"><span data-stu-id="0e73f-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="0e73f-217">Merhaba Zamanlayıcı işlev kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e73f-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="0e73f-218">Burada selamlama iletisine gönderilen Hello sıra adı girin:</span><span class="sxs-lookup"><span data-stu-id="0e73f-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="0e73f-219">Merhaba tıklatın  **+**  düğmesini kullandığınız önceden hello sıra tetikleyiciyle tooselect hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="0e73f-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="0e73f-220">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-220">Then click **Save**.</span></span>
8. <span data-ttu-id="0e73f-221">Merhaba tıklatın **geliştirme** Zamanlayıcı tetikleyicinizin sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0e73f-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="0e73f-222">İleti nesne adı daha önce gösterilen aynı sıraya hello kullanılan sürece hello C# Zamanlayıcı işlevi için koddan hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e73f-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="0e73f-223">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e73f-223">Then click **Save**.</span></span>

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

<span data-ttu-id="0e73f-224">Bu noktada, hello örnek cron ifade kullandıysanız hello C# Zamanlayıcı işlevi her 30 saniyede yürütür.</span><span class="sxs-lookup"><span data-stu-id="0e73f-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="0e73f-225">Merhaba günlükleri hello Zamanlayıcı işlevi için her yürütme raporu:</span><span class="sxs-lookup"><span data-stu-id="0e73f-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="0e73f-226">Merhaba tarayıcı penceresinde hello sıra işlevi için işlenmekte olan her bir ileti görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e73f-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="0e73f-227">Kod ile işlevi test etme</span><span class="sxs-lookup"><span data-stu-id="0e73f-227">Test a function with code</span></span>
<span data-ttu-id="0e73f-228">İşlevlerinizi toocreate dış bir uygulama veya framework tootest gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0e73f-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="0e73f-229">Bir HTTP tetikleyicisi işlevini koduyla test: Node.js</span><span class="sxs-lookup"><span data-stu-id="0e73f-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="0e73f-230">Bir Node.js uygulaması tooexecute bir HTTP isteği tootest işlevinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e73f-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="0e73f-231">Tooset emin olun:</span><span class="sxs-lookup"><span data-stu-id="0e73f-231">Make sure tooset:</span></span>

* <span data-ttu-id="0e73f-232">Merhaba `host` hello isteği seçenekleri tooyour işlevi uygulama konaktaki.</span><span class="sxs-lookup"><span data-stu-id="0e73f-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="0e73f-233">Merhaba, işlev adı `path`.</span><span class="sxs-lookup"><span data-stu-id="0e73f-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="0e73f-234">Erişim kodunuzu (`<your code>`) hello içinde `path`.</span><span class="sxs-lookup"><span data-stu-id="0e73f-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="0e73f-235">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="0e73f-235">Code example:</span></span>

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


<span data-ttu-id="0e73f-236">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="0e73f-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="0e73f-237">Merhaba portalında **günlükleri** penceresinde, çıktı benzer toohello aşağıdaki hello işlev yürütülürken kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="0e73f-238">Bir kuyruk tetikleyici işlevini koduyla test: C#</span><span class="sxs-lookup"><span data-stu-id="0e73f-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="0e73f-239">Kuyrukta kod toodrop bir ileti kullanarak bir sıra tetikleyici test edebilirsiniz daha önce bahsedilen.</span><span class="sxs-lookup"><span data-stu-id="0e73f-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="0e73f-240">Aşağıdaki kod örneği hello hello sunulan hello C# kod temel [Azure kuyruk depolamaya başlama](../storage/queues/storage-dotnet-how-to-use-queues.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="0e73f-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="0e73f-241">Kod diğer diller için de bu bağlantıdan bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0e73f-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="0e73f-242">tootest bu kodu bir konsol uygulamasında yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e73f-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="0e73f-243">[Merhaba app.config dosyasında depolama bağlantı dizelerinizi yapılandırma](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="0e73f-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="0e73f-244">Geçirmek bir `name` ve `address` parametreleri toohello uygulama olarak.</span><span class="sxs-lookup"><span data-stu-id="0e73f-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="0e73f-245">Örneğin, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="0e73f-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="0e73f-246">(Bu kodu hello ad ve adres yeni bir kullanıcı için komut satırı bağımsız değişkenleri olarak çalışma zamanı sırasında kabul eder.)</span><span class="sxs-lookup"><span data-stu-id="0e73f-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="0e73f-247">Örnek C# kod:</span><span class="sxs-lookup"><span data-stu-id="0e73f-247">Example C# code:</span></span>

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

<span data-ttu-id="0e73f-248">Merhaba tarayıcı penceresinde hello sıra işlevi için işlenmekte olan her bir ileti görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e73f-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure portal]: https://portal.azure.com
