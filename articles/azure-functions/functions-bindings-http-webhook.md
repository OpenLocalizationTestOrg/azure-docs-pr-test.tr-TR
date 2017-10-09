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
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="b2d1e-104">Azure işlevleri HTTP ve Web kancası bağlamaları</span><span class="sxs-lookup"><span data-stu-id="b2d1e-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b2d1e-105">Bu makale, tooconfigure ve iş HTTP ile nasıl tetikler açıklar ve Azure işlevlerinde bağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="b2d1e-106">Bu, Azure işlevleri toobuild sunucusuz API'ler ve yanıt toowebhooks kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="b2d1e-107">Azure işlevleri bağlamaları aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="b2d1e-108">Bir [HTTP tetikleyicisini](#httptrigger) bir HTTP isteğiyle bir işlevi çağırmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="b2d1e-109">Bu özelleştirilmiş toorespond çok olabilir[kancalarını](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="b2d1e-110">Bir [HTTP bağlama çıktı](#output) toorespond toohello istek sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="b2d1e-111">HTTP tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="b2d1e-111">HTTP trigger</span></span>
<span data-ttu-id="b2d1e-112">Merhaba HTTP tetikleyicisini işlevinizin yanıt tooan HTTP istek yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="b2d1e-113">Toorespond tooa belirli URL veya HTTP yöntemleri kümesini özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="b2d1e-114">Bir HTTP tetikleyicisi yapılandırılmış toorespond toowebhooks de olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="b2d1e-115">Hello işlevleri portalı kullanıyorsanız, aynı zamanda hemen önceden yapılmış bir şablon kullanarak başlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="b2d1e-116">Seçin **yeni işlev** ve "API & Web Kancalarını" Merhaba **senaryo** açılır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="b2d1e-117">Merhaba şablonlardan birini seçin ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="b2d1e-118">Varsayılan olarak, bir HTTP tetikleyicisi toohello isteği bir HTTP 200 Tamam durum kodu ve boş bir gövde ile yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="b2d1e-119">toomodify Merhaba yanıt, yapılandırma bir [HTTP çıktı bağlama](#output)</span><span class="sxs-lookup"><span data-stu-id="b2d1e-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="b2d1e-120">Bir HTTP tetikleyicisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2d1e-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="b2d1e-121">Bir HTTP tetikleyicisi hello aşağıdaki JSON nesnesi benzer bir toohello de dahil olmak üzere tarafından tanımlanan `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

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
<span data-ttu-id="b2d1e-122">Merhaba bağlama aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="b2d1e-123">**ad** : gerekli - işlev kodu hello istek veya istek gövdesi için kullanılan hello değişken adı.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="b2d1e-124">Bkz: [bir HTTP tetikleyicisi koddan çalışan](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="b2d1e-125">**tür** : gerekli - çok ayarlanmış olmalıdır "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="b2d1e-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="b2d1e-126">**Yön** : gerekli - çok "içinde" ayarlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="b2d1e-127">_authLevel_ : Bu hangi anahtarları varsa, toobe sipariş tooinvoke hello işlevinde hello istekte mevcut gereksinim belirler.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="b2d1e-128">Bkz: [anahtarlarla çalışma](#keys) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="b2d1e-129">Merhaba değer hello aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="b2d1e-130">_Anonim_: Hayır API anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="b2d1e-131">_işlev_: bir işleve özgü API anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="b2d1e-132">Hiçbiri sağlanmazsa hello varsayılan değer budur.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="b2d1e-133">_Yönetici_ : hello ana anahtar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="b2d1e-134">**yöntemleri** : Bu toowhich hello işlevi yanıt hello HTTP yöntemleri dizisidir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="b2d1e-135">Belirtilmezse, hello işlevi tooall HTTP yöntemleri yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="b2d1e-136">Bkz: [hello HTTP uç noktası özelleştirme](#url).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b2d1e-137">**Rota** : Bu toowhich denetleme hello rota şablonu tanımlar işlevinizin yanıt URL'leri isteyin.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="b2d1e-138">Merhaba hiçbiri sağlanmazsa varsayılan değer: `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="b2d1e-139">Bkz: [hello HTTP uç noktası özelleştirme](#url).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b2d1e-140">**webHookType** : hello HTTP tetikleyicisi tooact bu hello belirtilen sağlayıcı için bir Web kancası reciever olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="b2d1e-141">Merhaba _yöntemleri_ özelliği, değil Bu seçilirse ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="b2d1e-142">Bkz: [yanıt toowebhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="b2d1e-143">Merhaba değer hello aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="b2d1e-144">_genericJson_ : belirli bir sağlayıcı için mantığı olmadan bir genel amaçlı Web kancası uç noktası.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="b2d1e-145">_github_ : hello işlevi tooGitHub kancalarını yanıt verecektir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="b2d1e-146">Merhaba _authLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="b2d1e-147">_kayma_ : hello işlevi tooSlack kancalarını yanıt verecektir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="b2d1e-148">Merhaba _authLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="b2d1e-149">Bir HTTP tetikleyicisi kodu ile çalışma</span><span class="sxs-lookup"><span data-stu-id="b2d1e-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="b2d1e-150">C# ve F # işlevleri için tetikleyici giriş toobe hello türü ya da bildirebilirsiniz `HttpRequestMessage` veya özel bir tür.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="b2d1e-151">Seçerseniz `HttpRequestMessage`, tam erişim toohello istek nesnesi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="b2d1e-152">İçin özel bir tür (örneğin, bir POCO) işlevleri tooparse hello istek gövdesinde JSON toopopulate hello nesne özellikleri çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="b2d1e-153">Node.js işlevleri için hello işlevleri çalışma zamanı hello istek gövdesi yerine hello istek nesnesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="b2d1e-154">Bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) örneğin kullanımları.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="b2d1e-155">HTTP yanıtının çıkış bağlama</span><span class="sxs-lookup"><span data-stu-id="b2d1e-155">HTTP response output binding</span></span>
<span data-ttu-id="b2d1e-156">Merhaba HTTP çıkış bağlama toorespond toohello HTTP isteği gönderen kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="b2d1e-157">Bu bağlamanın bir HTTP tetikleyicisi gerektirir ve hello tetikleyicinin istekle ilişkili toocustomize hello yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="b2d1e-158">Bir HTTP bağlaması çıktı bir HTTP tetikleyicisi boş bir gövde ile HTTP 200 Tamam döndürmeyecektir sağlanan olur.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="b2d1e-159">Bir HTTP yapılandırma bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="b2d1e-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="b2d1e-160">Merhaba HTTP çıktı bağlama hello aşağıdaki JSON nesnesi benzer bir toohello dahil ederek tanımlanmış `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="b2d1e-161">Merhaba bağlama hello aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="b2d1e-162">**ad** : hello yanıtı işlevi kod içinde kullanılan değişken adı gerekli - hello.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="b2d1e-163">Bkz: [bir HTTP ile çalışma çıktı kodundan bağlama](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="b2d1e-164">**tür** : gerekli - çok ayarlanmış olmalıdır "http".</span><span class="sxs-lookup"><span data-stu-id="b2d1e-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="b2d1e-165">**Yön** : gerekli - çok "out" ayarlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="b2d1e-166">Bir HTTP ile çalışma kodundan bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="b2d1e-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="b2d1e-167">Http veya Web kancası hello çıkış parametresi (örneğin, "res") toorespond toohello arayan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="b2d1e-168">Alternatif olarak, standart kullanabilirsiniz `Request.CreateResponse()` (C#) veya `context.res` (Node.JS) deseni tooreturn yanıt.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="b2d1e-169">Nasıl toouse hello ikinci yöntemi ile ilgili örnekler için bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) ve [Web kancası tetikleyici örnekleri](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="b2d1e-170">Toowebhooks yanıt</span><span class="sxs-lookup"><span data-stu-id="b2d1e-170">Responding toowebhooks</span></span>
<span data-ttu-id="b2d1e-171">Bir HTTP tetikleyicisi hello ile _webHookType_ özelliği olacaktır yapılandırılmış toorespond çok[kancalarını](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="b2d1e-172">Merhaba temel yapılandırma hello "genericJson" ayarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="b2d1e-173">İstekleri tooonly olanlar HTTP POST ve hello kullanarak bu sınırlar `application/json` içerik türü.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="b2d1e-174">Merhaba tetikleyici ayrıca uyarlanmış tooa belirli Web kancası sağlayıcı olabilir (örneğin, [GitHub](https://developer.github.com/webhooks/) ve [Slack'e](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="b2d1e-175">Bir sağlayıcı belirtilmemişse hello işlevleri çalışma zamanı hello sağlayıcının doğrulama mantığını sizin için dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="b2d1e-176">GitHub Web kancası sağlayıcısı olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2d1e-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="b2d1e-177">toorespond tooGitHub kancalarını, önce bir HTTP tetikleyicisi ile işlevinizi oluşturun ve ayarlayın hello _webHookType_ özelliği çok "github".</span><span class="sxs-lookup"><span data-stu-id="b2d1e-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="b2d1e-178">Ardından kopyalama kendi [URL](#url) ve [API anahtarı](#keys) GitHub deponun içine **Web kancası eklemek** sayfası.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="b2d1e-179">GitHub'ınızın bkz [Web kancası oluşturma](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) daha fazla bilgi için belgeleri.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="b2d1e-180">Bir Web kancası sağlayıcısı olarak kayma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2d1e-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="b2d1e-181">Merhaba Slack Web kancası işlevi özel bir anahtar kayma hello belirtecinden ile yapılandırmanız gerekir, belirtmenize izin verir yerine bir belirteç sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="b2d1e-182">Bkz: [anahtarlarla çalışma](#keys).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="b2d1e-183">Merhaba HTTP uç noktası özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b2d1e-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="b2d1e-184">Bir HTTP tetikleyicisi ya da Web kancası, bir işlev oluşturduğunuzda varsayılan olarak hello işlevi adreslenebilir hello formunun bir yol şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="b2d1e-185">İsteğe bağlı hello kullanarak bu yolun özelleştirebilirsiniz `route` hello HTTP tetikleyicisi özellikte bağlama girdisini.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="b2d1e-186">Aşağıdaki örnek olarak, hello *function.json* dosya tanımlayan bir `route` özelliği bir HTTP tetikleyicisi için:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="b2d1e-187">Bu yapılandırma, hello işlevi artık rota hello özgün yol yerine aşağıdaki hello ile adreslenebilir kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="b2d1e-188">Bu, toosupport iki parametrelerinde hello adresi, "kategorisi" ve "id" Merhaba işlev kodu sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="b2d1e-189">Kullanabilirsiniz [Web API rota kısıtlaması](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) , parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="b2d1e-190">C# işlev kodu aşağıdaki Merhaba parametrelerinin her ikisini de kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-190">hello following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="b2d1e-191">Aynı yol parametreleri Node.js işlevi kod toouse hello aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-191">Here is Node.js function code toouse hello same route parameters.</span></span>

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

<span data-ttu-id="b2d1e-192">Varsayılan olarak, tüm işlevi yollar ile önek *API*.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="b2d1e-193">Ayrıca özelleştirme veya hello kullanan hello öneki kaldırın `http.routePrefix` özelliğinde, *host.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="b2d1e-194">Merhaba aşağıdaki örnek kaldırır hello *API* hello hello önekini için boş bir dize kullanarak rota öneki *host.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="b2d1e-195">Hakkında ayrıntılı bilgi için tooupdate hello *host.json* bakın, işlevinizi dosyası [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="b2d1e-196">Diğer özellikler hakkında bilgi için yapılandırabileceğiniz, *host.json* dosya için bkz: [host.json başvuru](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="b2d1e-197">Anahtarları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="b2d1e-197">Working with keys</span></span>
<span data-ttu-id="b2d1e-198">HttpTriggers ek güvenlik için anahtarları yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="b2d1e-199">Standart HttpTrigger hello anahtar toobe hello istekte mevcut gerektiren bir API anahtarı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="b2d1e-200">Web kancası anahtarları tooauthorize isteklerini bir hangi hello sağlayıcının desteklediği bağlı olarak, çeşitli şekillerde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="b2d1e-201">Anahtarları azure'da işlevi uygulamanız bir parçası olarak depolanır ve bekleyen şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="b2d1e-202">tooview, anahtarlarınızı yenilerini oluşturun veya toplama anahtarları toonew değerleri, işlevlerinizi hello portalındaki tooone gidin ve "Manage" seçin</span><span class="sxs-lookup"><span data-stu-id="b2d1e-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="b2d1e-203">Anahtarların iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-203">There are two types of keys:</span></span>
- <span data-ttu-id="b2d1e-204">**Ana bilgisayar anahtarları**: Bu anahtarları hello işlevi uygulamasında tüm işlevleri tarafından paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="b2d1e-205">Bir API anahtarı olarak kullanıldığında, bunlar erişim tooany işlevi hello işlevi uygulama içinde izin verir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="b2d1e-206">**İşlev tuşları**: Bu anahtarların bunlar tanımlanan yalnızca toohello belirli işlevler Uygula.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="b2d1e-207">Bunlar yalnızca, bir API anahtarı olarak kullanıldığında, erişim toothat işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="b2d1e-208">Her anahtar için başvuru olarak adlandırılır ve hello işlevi ve ana bilgisayar düzeyinde ("varsayılan" adlı) bir varsayılan anahtar yok.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="b2d1e-209">Merhaba **ana anahtar** varsayılan ana bilgisayar anahtarı "her işlev uygulaması için tanımlanır ve iptal edilemiyor _master" olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="b2d1e-210">Yönetim erişimi toohello çalışma zamanı API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="b2d1e-211">Kullanarak `"authLevel": "admin"` hello JSON bağlama hello istek üzerine sunulan bu anahtar toobe gerekir; başka bir anahtar bir yetkilendirme hatasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="b2d1e-212">Son toohello yükseltilmiş hello ana anahtar ile bu anahtarı üçüncü taraflarla paylaşma veya gerekir yerel istemci uygulamalarında dağıtmak izinler.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="b2d1e-213">Hello Yöneticisi yetki düzeyini seçerken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="b2d1e-214">API anahtarı yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="b2d1e-214">API key authorization</span></span>
<span data-ttu-id="b2d1e-215">Varsayılan olarak, bir HttpTrigger hello HTTP isteği bir API anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="b2d1e-216">Bu nedenle, HTTP isteği normalde şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="b2d1e-217">Merhaba anahtar adlı bir sorgu dizesi değişkeni dahil edilebilir `code`, yukarıdaki olarak veya içinde eklenebilir bir `x-functions-key` HTTP üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="b2d1e-218">Merhaba hello anahtarının değerini hello işlev için tanımlanmış herhangi bir işlev tuşu veya tüm ana bilgisayar anahtarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="b2d1e-219">Anahtarları olmadan tooallow isteklerin seçin veya bu hello ana anahtar hello değiştirerek kullanılmalıdır belirtin `authLevel` JSON bağlama hello özelliğinde (bkz [HTTP tetikleyicisini](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="b2d1e-220">Anahtarlar ve Web kancaları</span><span class="sxs-lookup"><span data-stu-id="b2d1e-220">Keys and webhooks</span></span>
<span data-ttu-id="b2d1e-221">Web kancası yetkilendirme hello Web kancası reciever bileşeni tarafından yapılır, hello HttpTrigger ve hello mekanizması parçası hello Web kancası türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="b2d1e-222">Her mekanizması yok, ancak bir anahtar kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="b2d1e-223">Varsayılan olarak, "varsayılan" adlı hello işlevi anahtar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="b2d1e-224">Farklı bir anahtar toouse isterseniz tooconfigure hello Web kancası sağlayıcı toosend hello anahtar adı hello istek yolu izleyerek hello birinde ile gerekir:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="b2d1e-225">**Sorgu dizesi**: hello sağlayıcısı hello hello anahtar adı geçen `clientid` sorgu dizesi parametresi (örneğin, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="b2d1e-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="b2d1e-226">**İstek üst bilgisi**: hello sağlayıcısı hello hello anahtar adı geçen `x-functions-clientid` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="b2d1e-227">İşlev tuşları, ana bilgisayar anahtarları önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="b2d1e-228">İki anahtar ile aynı adı, hello hello tanımlanmışsa, işlev tuşu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="b2d1e-229">HTTP tetikleyicisi örnekleri</span><span class="sxs-lookup"><span data-stu-id="b2d1e-229">HTTP trigger samples</span></span>
<span data-ttu-id="b2d1e-230">Merhaba, HTTP tetikleyicisini aşağıdaki hello olduğunu varsayalım `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="b2d1e-231">Arar hello dile özgü örnek bkz bir `name` parametresi hello sorgu dizesi veya hello hello HTTP istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="b2d1e-232">C#</span><span class="sxs-lookup"><span data-stu-id="b2d1e-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="b2d1e-233">F#</span><span class="sxs-lookup"><span data-stu-id="b2d1e-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="b2d1e-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="b2d1e-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="b2d1e-235">HTTP tetikleyicisi örnek C#</span><span class="sxs-lookup"><span data-stu-id="b2d1e-235">HTTP trigger sample in C#</span></span> #
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

<span data-ttu-id="b2d1e-236">Tooa POCO de bağlayabilirsiniz yerine `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="b2d1e-237">Bu hello isteği, JSON olarak ayrıştırılır hello gövdesi gelen hydrated.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="b2d1e-238">Benzer şekilde, bir tür bağlama toohello HTTP yanıt çıktısı geçirilebilir ve bu 200 durum koduyla hello yanıt gövdesi olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="b2d1e-239">F # HTTP tetikleyicisi örnek</span><span class="sxs-lookup"><span data-stu-id="b2d1e-239">HTTP trigger sample in F#</span></span> #
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

<span data-ttu-id="b2d1e-240">Gereksinim duyduğunuz bir `project.json` NuGet tooreference hello kullanan bir dosyayı `FSharp.Interop.Dynamic` ve `Dynamitey` derlemeler şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="b2d1e-241">Bu, NuGet toofetch bağımlılıklarınızı kullanacak ve bunları komut dosyanıza başvurur.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="b2d1e-242">Node.JS HTTP tetikleyicisi örnek</span><span class="sxs-lookup"><span data-stu-id="b2d1e-242">HTTP trigger sample in Node.JS</span></span>
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
## <a name="webhook-samples"></a><span data-ttu-id="b2d1e-243">Web kancası örnekleri</span><span class="sxs-lookup"><span data-stu-id="b2d1e-243">Webhook samples</span></span>
<span data-ttu-id="b2d1e-244">Web kancası tetikleyici hello aşağıdaki hello olduğunu varsayalım `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b2d1e-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="b2d1e-245">GitHub sorunu yorum günlükleri hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="b2d1e-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="b2d1e-246">C#</span><span class="sxs-lookup"><span data-stu-id="b2d1e-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="b2d1e-247">F#</span><span class="sxs-lookup"><span data-stu-id="b2d1e-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="b2d1e-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="b2d1e-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="b2d1e-249">Web kancası örnek C#</span><span class="sxs-lookup"><span data-stu-id="b2d1e-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="b2d1e-250">Web kancası örnek F #</span><span class="sxs-lookup"><span data-stu-id="b2d1e-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="b2d1e-251">Node.JS Web kancası örnek</span><span class="sxs-lookup"><span data-stu-id="b2d1e-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="b2d1e-252">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2d1e-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

