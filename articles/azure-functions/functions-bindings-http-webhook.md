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
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="9b9a8-104">Azure işlevleri HTTP ve Web kancası bağlamaları</span><span class="sxs-lookup"><span data-stu-id="9b9a8-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="9b9a8-105">Bu makalede, yapılandırma ve HTTP Tetikleyicileri ve bağlamaları Azure işlevlerinde çalışmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="9b9a8-106">Bu konularda sunucusuz API'ları derleme ve Web kancası için yanıt vermek için Azure işlevleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="9b9a8-107">Azure işlevleri aşağıdaki bağlamaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="9b9a8-108">Bir [HTTP tetikleyicisini](#httptrigger) bir HTTP isteğiyle bir işlevi çağırmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="9b9a8-109">Bu yanıt için özelleştirilebilir [kancalarını](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="9b9a8-110">Bir [HTTP bağlama çıktı](#output) isteğine yanıt olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="9b9a8-111">HTTP tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="9b9a8-111">HTTP trigger</span></span>
<span data-ttu-id="9b9a8-112">HTTP tetikleyicisini işlevinizde bir HTTP isteğine yanıt olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="9b9a8-113">Belirli bir URL veya HTTP yöntemleri kümesini yanıt verecek şekilde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="9b9a8-114">Bir HTTP tetikleyicisi için Web kancası yanıt verecek şekilde de yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="9b9a8-115">İşlevler Portalı'nı kullanarak, siz de hemen önceden yapılmış bir şablon kullanarak başlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="9b9a8-116">Seçin **yeni işlev** ve "API & Web Kancalarını" arasından **senaryo** açılır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="9b9a8-117">Şablonlardan birini seçin ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="9b9a8-118">Varsayılan olarak, bir HTTP tetikleyicisi bir HTTP 200 Tamam durum kodu ve boş bir gövde ile isteğine yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="9b9a8-119">Yanıt değiştirmek için yapılandırma bir [HTTP çıktı bağlama](#output)</span><span class="sxs-lookup"><span data-stu-id="9b9a8-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="9b9a8-120">Bir HTTP tetikleyicisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b9a8-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="9b9a8-121">Bir HTTP tetikleyicisi aşağıdakine benzer bir JSON nesnesi de dahil olmak üzere tarafından tanımlanan `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

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
<span data-ttu-id="9b9a8-122">Bağlama aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="9b9a8-123">**ad** : gerekli - istek veya istek gövdesi için işlevi kod içinde kullanılan değişken adı.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="9b9a8-124">Bkz: [bir HTTP tetikleyicisi koddan çalışan](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="9b9a8-125">**tür** : gerekli - "httpTrigger" ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="9b9a8-126">**Yön** : gerekli - "için" kümesindeki olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="9b9a8-127">_authLevel_ : Bu anahtarları, varsa, işlevin çalıştırılabilmesi için istekte bulunması gerekenleri belirler.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="9b9a8-128">Bkz: [anahtarlarla çalışma](#keys) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="9b9a8-129">Değerin aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="9b9a8-130">_Anonim_: Hayır API anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="9b9a8-131">_işlev_: bir işleve özgü API anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="9b9a8-132">Bu, hiçbiri sağlanmazsa varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="9b9a8-133">_Yönetici_ : ana anahtar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="9b9a8-134">**yöntemleri** : Bu işlev yanıt için HTTP yöntemleri dizisidir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="9b9a8-135">Belirtilmezse, işlev tüm HTTP yöntemlerine yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="9b9a8-136">Bkz: [HTTP uç noktası özelleştirme](#url).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="9b9a8-137">**Rota** : Bu rota şablonu tanımlar, kendisine URL'leri isteği denetleme işlevinizin yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="9b9a8-138">Varsayılan değer hiçbiri sağlanmazsa `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="9b9a8-139">Bkz: [HTTP uç noktası özelleştirme](#url).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="9b9a8-140">**webHookType** : Bu, HTTP tetikleyicisini belirtilen sağlayıcı için bir Web kancası reciever davranacak şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="9b9a8-141">_Yöntemleri_ özelliği, değil Bu seçilirse ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="9b9a8-142">Bkz: [Web kancası için yanıt](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="9b9a8-143">Değerin aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="9b9a8-144">_genericJson_ : belirli bir sağlayıcı için mantığı olmadan bir genel amaçlı Web kancası uç noktası.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="9b9a8-145">_github_ : işlevi için GitHub Web kancası yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="9b9a8-146">_AuthLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="9b9a8-147">_kayma_ : işlevi Slack kancalarını yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="9b9a8-148">_AuthLevel_ özelliği, değil Bu seçilirse ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="9b9a8-149">Bir HTTP tetikleyicisi kodu ile çalışma</span><span class="sxs-lookup"><span data-stu-id="9b9a8-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="9b9a8-150">C# ve F # işlevleri için giriş aşağıdakilerden biri olması için tetikleyici türünü bildirebilir `HttpRequestMessage` veya özel bir tür.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="9b9a8-151">Seçerseniz `HttpRequestMessage`, istek nesnesi tam erişimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="9b9a8-152">İçin özel bir tür (örneğin, bir POCO) işlevleri istek gövdesi nesne özelliklerini doldurmak için JSON olarak ayrıştırılamıyor dener.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="9b9a8-153">Node.js işlevleri için işlevleri çalışma zamanı yerine request nesnesi istek gövdesinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="9b9a8-154">Bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) örneğin kullanımları.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="9b9a8-155">HTTP yanıtının çıkış bağlama</span><span class="sxs-lookup"><span data-stu-id="9b9a8-155">HTTP response output binding</span></span>
<span data-ttu-id="9b9a8-156">HTTP isteği gönderene yanıt bağlama HTTP çıkış kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="9b9a8-157">Bu bağlamanın bir HTTP tetikleyicisi gerektirir ve tetikleyici istekle ilişkili yanıt özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="9b9a8-158">Bir HTTP bağlaması çıktı bir HTTP tetikleyicisi boş bir gövde ile HTTP 200 Tamam döndürmeyecektir sağlanan olur.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="9b9a8-159">Bir HTTP yapılandırma bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="9b9a8-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="9b9a8-160">HTTP çıkış bağlama aşağıdakine benzer bir JSON nesnesi ekleyerek tanımlanmış `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="9b9a8-161">Bağlama aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="9b9a8-162">**ad** : gerekli - yanıt işlevi kod içinde kullanılan değişken adı.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="9b9a8-163">Bkz: [bir HTTP ile çalışma çıktı kodundan bağlama](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="9b9a8-164">**tür** : gerekli - "http" olarak ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="9b9a8-165">**Yön** : gerekli - out"için" ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="9b9a8-166">Bir HTTP ile çalışma kodundan bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="9b9a8-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="9b9a8-167">Http veya Web kancası çağırana yanıt için çıktı parametresi (örneğin, "res") kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="9b9a8-168">Alternatif olarak, standart kullanabilirsiniz `Request.CreateResponse()` (C#) veya `context.res` yanıtınız döndürülecek (Node.JS) deseni.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="9b9a8-169">İkinci yöntemi kullanma hakkında daha fazla örnekler için bkz: [HTTP tetikleyicisi örnekleri](#httptriggersample) ve [Web kancası tetikleyici örnekleri](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="9b9a8-170">Web kancası için yanıt</span><span class="sxs-lookup"><span data-stu-id="9b9a8-170">Responding to webhooks</span></span>
<span data-ttu-id="9b9a8-171">Bir HTTP tetikleyicisi ile _webHookType_ özelliği, yanıt verecek şekilde yapılandırılacak [kancalarını](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="9b9a8-172">Temel yapılandırma "genericJson" ayarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="9b9a8-173">Bu istekleri yalnızca HTTP POST ile ile kısıtlayan `application/json` içerik türü.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="9b9a8-174">Tetikleyici için bir özel Web kancası sağlayıcısı ayrıca uyarlanabilir (örn., [GitHub](https://developer.github.com/webhooks/) ve [Slack'e](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="9b9a8-175">Bir sağlayıcı belirtilmemişse işlevleri çalışma zamanı sağlayıcının doğrulama mantığını sizin için dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="9b9a8-176">GitHub Web kancası sağlayıcısı olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b9a8-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="9b9a8-177">GitHub Web kancası için yanıt vermek için önce bir HTTP tetikleyicisi ile işlevinizi oluşturma ve ayarlama _webHookType_ "github" özelliğine.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="9b9a8-178">Ardından kopyalama kendi [URL](#url) ve [API anahtarı](#keys) GitHub deponun içine **Web kancası eklemek** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="9b9a8-179">GitHub'ınızın bkz [Web kancası oluşturma](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) daha fazla bilgi için belgeleri.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="9b9a8-180">Bir Web kancası sağlayıcısı olarak kayma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b9a8-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="9b9a8-181">Slack Web kancası işlevi özel bir anahtar kayma belirtecinden ile yapılandırmanız gerekir, belirtmenize izin verir yerine bir belirteç sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="9b9a8-182">Bkz: [anahtarlarla çalışma](#keys).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="9b9a8-183">HTTP uç noktası özelleştirme</span><span class="sxs-lookup"><span data-stu-id="9b9a8-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="9b9a8-184">Bir HTTP tetikleyicisi ya da Web kancası, bir işlev oluşturduğunuzda varsayılan olarak işlevi adreslenebilir biçiminde bir yol şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="9b9a8-185">İsteğe bağlı kullanarak bu yolun özelleştirebilirsiniz `route` HTTP tetikleyicisini özellikte bağlama girdisini.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="9b9a8-186">Örneğin, aşağıdaki *function.json* dosya tanımlayan bir `route` özelliği bir HTTP tetikleyicisi için:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="9b9a8-187">Bu yapılandırma, işlevi artık özgün yol yerine aşağıdaki yol ile adreslenebilir kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="9b9a8-188">Bu adres, "kategorisi" ve "id" iki parametrelerini desteklemek işlev kodu sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="9b9a8-189">Kullanabilirsiniz [Web API rota kısıtlaması](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) , parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="9b9a8-190">Aşağıdaki C# işlevi kodu her iki parametrelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-190">The following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="9b9a8-191">Burada, aynı rota parametrelerini kullanmak için Node.js işlev kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-191">Here is Node.js function code to use the same route parameters.</span></span>

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

<span data-ttu-id="9b9a8-192">Varsayılan olarak, tüm işlevi yollar ile önek *API*.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="9b9a8-193">Ayrıca özelleştirme veya önek kullanarak kaldırma `http.routePrefix` özelliğinde, *host.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="9b9a8-194">Aşağıdaki örnek kaldırır *API* önekini için boş bir dize kullanarak rota öneki *host.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="9b9a8-195">Güncelleştirme hakkında ayrıntılı bilgi için *host.json* bakın, işlevinizi dosyası [işlevi uygulama dosyaları güncelleştirmek nasıl](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="9b9a8-196">Diğer özellikler hakkında bilgi için yapılandırabileceğiniz, *host.json* dosya için bkz: [host.json başvuru](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="9b9a8-197">Anahtarları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="9b9a8-197">Working with keys</span></span>
<span data-ttu-id="9b9a8-198">HttpTriggers ek güvenlik için anahtarları yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="9b9a8-199">Standart HttpTrigger istekte bulunması için anahtar gerektiren bir API anahtarı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="9b9a8-200">Web kancası bir ne sağlayıcının desteklediği bağlı olarak, çeşitli şekillerde isteklerinde yetkilendirmek için tuşlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="9b9a8-201">Anahtarları azure'da işlevi uygulamanız bir parçası olarak depolanır ve bekleyen şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="9b9a8-202">Anahtarlarınızı görüntülemek için yeni bir tane oluşturun veya anahtarları alma yeni değerler, işlevlerinizi portalındaki birine gidin ve "Manage" seçin</span><span class="sxs-lookup"><span data-stu-id="9b9a8-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="9b9a8-203">Anahtarların iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-203">There are two types of keys:</span></span>
- <span data-ttu-id="9b9a8-204">**Ana bilgisayar anahtarları**: Bu anahtarları işlevi uygulamasında tüm işlevleri tarafından paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="9b9a8-205">Bir API anahtarı olarak kullanıldığında, bu işlev uygulaması içinde herhangi bir işlev erişime izin verin.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="9b9a8-206">**İşlev tuşları**: Bu anahtarları altında bunların tanımlanan yalnızca belirli işlevler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="9b9a8-207">Bunlar yalnızca, bir API anahtarı olarak kullanıldığında, bu işlev erişime izin ver.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="9b9a8-208">Her anahtar için başvuru olarak adlandırılır ve işlev ve ana bilgisayar düzeyinde ("varsayılan" adlı) bir varsayılan anahtar yok.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="9b9a8-209">**Ana anahtar** varsayılan ana bilgisayar anahtarı "her işlev uygulaması için tanımlanır ve iptal edilemiyor _master" olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="9b9a8-210">Çalışma zamanı API yönetim erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="9b9a8-211">Kullanarak `"authLevel": "admin"` bağlamasında JSON isteği sunulması için bu anahtar gerekir; başka bir anahtar bir yetkilendirme hatasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="9b9a8-212">Ana anahtar ile yükseltilmiş izinler nedeniyle, bu anahtarı üçüncü taraflarla paylaşma veya gerekir yerel istemci uygulamalarında dağıtın.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="9b9a8-213">Yönetici yetki düzeyini seçerken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="9b9a8-214">API anahtarı yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="9b9a8-214">API key authorization</span></span>
<span data-ttu-id="9b9a8-215">Varsayılan olarak, bir HttpTrigger HTTP isteği bir API anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="9b9a8-216">Bu nedenle, HTTP isteği normalde şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="9b9a8-217">Anahtar adlı bir sorgu dizesi değişkeni dahil edilebilir `code`, yukarıdaki olarak veya içinde eklenebilir bir `x-functions-key` HTTP üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="9b9a8-218">Anahtarın değerini işlevi için tanımlanan herhangi bir işlev tuşu veya tüm ana bilgisayar anahtarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="9b9a8-219">Anahtarları olmadan isteklere izin vermek veya ana anahtarı değiştirerek kullanılması gerektiğini belirtmek seçebileceğiniz `authLevel` JSON bağlama özelliğinde (bkz [HTTP tetikleyicisini](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="9b9a8-220">Anahtarlar ve Web kancaları</span><span class="sxs-lookup"><span data-stu-id="9b9a8-220">Keys and webhooks</span></span>
<span data-ttu-id="9b9a8-221">Web kancası yetkilendirme Web kancası reciever bileşeni tarafından HttpTrigger parçası işlenir ve mekanizması Web kancası türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="9b9a8-222">Her mekanizması yok, ancak bir anahtar kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="9b9a8-223">Varsayılan olarak, "varsayılan" adlı işlevi anahtar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="9b9a8-224">Farklı bir anahtarı kullanmak istiyorsanız, aşağıdaki yollardan biriyle istek anahtarı adıyla göndermek için Web kancası sağlayıcısı yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="9b9a8-225">**Sorgu dizesi**: anahtar adına Sağlayıcının geçirdiği `clientid` sorgu dizesi parametresi (örneğin, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="9b9a8-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="9b9a8-226">**İstek üst bilgisi**: anahtar adına Sağlayıcının geçirdiği `x-functions-clientid` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="9b9a8-227">İşlev tuşları, ana bilgisayar anahtarları önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="9b9a8-228">Aynı ada sahip iki anahtar tanımlanmışsa işlevi anahtar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="9b9a8-229">HTTP tetikleyicisi örnekleri</span><span class="sxs-lookup"><span data-stu-id="9b9a8-229">HTTP trigger samples</span></span>
<span data-ttu-id="9b9a8-230">Aşağıdaki HTTP tetikleyicisini olduğunu varsayalım `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="9b9a8-231">Arar dile özgü örnek bkz bir `name` parametresi sorgu dizesi veya HTTP istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="9b9a8-232">C#</span><span class="sxs-lookup"><span data-stu-id="9b9a8-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="9b9a8-233">F#</span><span class="sxs-lookup"><span data-stu-id="9b9a8-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="9b9a8-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="9b9a8-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="9b9a8-235">HTTP tetikleyicisi örnek C#</span><span class="sxs-lookup"><span data-stu-id="9b9a8-235">HTTP trigger sample in C#</span></span> #
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

<span data-ttu-id="9b9a8-236">POCO yerine de bağlayabilirsiniz `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="9b9a8-237">Bu JSON olarak ayrıştırılır, istek gövdesinden hydrated.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="9b9a8-238">Benzer şekilde, bir tür bağlama HTTP yanıt çıkışı geçirilebilir ve bu 200 durum koduyla yanıt gövdesi olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="9b9a8-239">F # HTTP tetikleyicisi örnek</span><span class="sxs-lookup"><span data-stu-id="9b9a8-239">HTTP trigger sample in F#</span></span> #
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

<span data-ttu-id="9b9a8-240">Gereksinim duyduğunuz bir `project.json` NuGet başvurmak için kullanılan dosya `FSharp.Interop.Dynamic` ve `Dynamitey` derlemeler şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="9b9a8-241">Bu NuGet bağımlılıklarınızı getirilemedi kullanacak ve bunları komut dosyanıza başvurur.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="9b9a8-242">Node.JS HTTP tetikleyicisi örnek</span><span class="sxs-lookup"><span data-stu-id="9b9a8-242">HTTP trigger sample in Node.JS</span></span>
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
## <a name="webhook-samples"></a><span data-ttu-id="9b9a8-243">Web kancası örnekleri</span><span class="sxs-lookup"><span data-stu-id="9b9a8-243">Webhook samples</span></span>
<span data-ttu-id="9b9a8-244">Aşağıdaki Web kancası tetikleyici olduğunu varsayalım `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="9b9a8-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="9b9a8-245">GitHub sorunu yorum günlükleri dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="9b9a8-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="9b9a8-246">C#</span><span class="sxs-lookup"><span data-stu-id="9b9a8-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="9b9a8-247">F#</span><span class="sxs-lookup"><span data-stu-id="9b9a8-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="9b9a8-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="9b9a8-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="9b9a8-249">Web kancası örnek C#</span><span class="sxs-lookup"><span data-stu-id="9b9a8-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="9b9a8-250">Web kancası örnek F #</span><span class="sxs-lookup"><span data-stu-id="9b9a8-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="9b9a8-251">Node.JS Web kancası örnek</span><span class="sxs-lookup"><span data-stu-id="9b9a8-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="9b9a8-252">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9b9a8-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

