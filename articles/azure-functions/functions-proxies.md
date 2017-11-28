---
title: "Azure işlevleri proxy'leri ile aaaWork | Microsoft Docs"
description: "Hakkında genel bakış toouse Azure işlevleri proxy'leri"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="7b0ff-103">Azure işlevleri proxy'leri (Önizleme) ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7b0ff-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="7b0ff-104">Azure işlevleri proxy'leri şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="7b0ff-105">Önizleme, ancak standart işlevleri faturalama tooproxy yürütmeleri uygularken ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="7b0ff-106">Daha fazla bilgi için bkz: [Azure işlevleri fiyatlandırma](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="7b0ff-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="7b0ff-107">Bu makalede açıklanır nasıl tooconfigure ve Azure işlevleri proxy'leri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="7b0ff-108">Bu özellik ile başka bir kaynak tarafından uygulanan işlevi uygulamanızdan uç noktalarını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="7b0ff-109">İstemciler için tek bir API yüzeyi hala sunarken büyük bir API uygulamasına (olduğu gibi bir mikro Hizmet Mimarisi), birden çok işlev uygulamalarının bu proxy'leri toobreak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="7b0ff-110"><a name="enable"></a>Azure işlevleri proxy'leri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7b0ff-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="7b0ff-111">Proxy'leri varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="7b0ff-112">Merhaba özellik devre dışı bırakıldı, ancak bunlar yürütülemeyecek proxy'leri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="7b0ff-113">tooenable proxy'leri hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="7b0ff-114">Açık hello [Azure portal], ve ardından tooyour işlev uygulaması gidin.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="7b0ff-115">Seçin **işlev uygulaması ayarları**.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="7b0ff-116">Anahtar **etkinleştirmek Azure işlevleri proxy'leri (Önizleme)** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="7b0ff-117">Yeni özellikleri kullanılabilir duruma geldiğinde tooupdate hello proxy çalışma zamanı Ayrıca buraya dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="7b0ff-118"><a name="create"></a>Bir proxy sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b0ff-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="7b0ff-119">Bu bölümde, nasıl toocreate proxy'sine bir hello işlevleri portalına gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="7b0ff-120">Açık hello [Azure portal], ve ardından tooyour işlev uygulaması gidin.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="7b0ff-121">Merhaba sol bölmesinde seçin **yeni proxy**.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="7b0ff-122">Proxy için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="7b0ff-123">Merhaba belirterek bu işlev uygulaması sunulan hello uç noktası yapılandırmak **rota şablonu** ve **HTTP yöntemleri**.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="7b0ff-124">Bu parametreler için according toohello kuralları davranır [HTTP Tetikleyicileri].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="7b0ff-125">Set hello **arka uç URL'si** tooanother uç noktası.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="7b0ff-126">Bu uç noktaya başka bir işlev uygulaması işlevinde olabilir veya diğer herhangi bir API'yi olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="7b0ff-127">Merhaba değeri toobe statik gerekmez ve başvurusu yapabilir [uygulama ayarları] ve [hello özgün istemci istek parametrelerinden].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="7b0ff-128">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-128">Click **Create**.</span></span>

<span data-ttu-id="7b0ff-129">Proxy şimdi işlevi uygulamanızdan yeni bir uç noktası olarak bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="7b0ff-130">İstemci açısından bakıldığında, bu eşdeğer tooan Azure işlevlerinde HttpTrigger olur.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="7b0ff-131">Merhaba Proxy URL'si kopyalayarak ve sık kullanılan HTTP istemci ile test yeni proxy deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="7b0ff-132"><a name="modify-requests-responses"></a>İsteklerin ve yanıtların değiştirme</span><span class="sxs-lookup"><span data-stu-id="7b0ff-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="7b0ff-133">Azure işlevleri proxy'leriyle istekleri tooand yanıtları hello arka uçtan değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="7b0ff-134">Bu dönüşümleri tanımlandığı gibi değişkenleri kullanabilirsiniz [değişkenlerini kullanın].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="7b0ff-135"><a name="modify-backend-request"></a>Merhaba arka uç isteği değiştirme</span><span class="sxs-lookup"><span data-stu-id="7b0ff-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="7b0ff-136">Varsayılan olarak, hello arka uç isteği hello özgün istek bir kopyası olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="7b0ff-137">Ayrıca toosetting hello arka uç URL'si, değişiklikleri toohello HTTP yöntemi, üst bilgiler ve sorgu dizesi parametreleri yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="7b0ff-138">Merhaba değiştirilen değerleri başvuru [uygulama ayarları] ve [hello özgün istemci istek parametrelerinden].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="7b0ff-139">Şu anda arka uç istekleri değiştirmek için hiçbir portal deneyimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="7b0ff-140">toolearn tooapply proxies.json, bu özellikten nasıl görürüm [requestOverrides nesnesi tanımlayın].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="7b0ff-141"><a name="modify-response"></a>Merhaba yanıtı değiştirebilir</span><span class="sxs-lookup"><span data-stu-id="7b0ff-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="7b0ff-142">Varsayılan olarak, hello istemci yanıt hello arka uç yanıt bir kopyası olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="7b0ff-143">Değişiklikleri toohello yanıtın durum kodu, neden ifadesini, üstbilgiler ve gövde yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="7b0ff-144">Merhaba değiştirilen değerleri başvuru [uygulama ayarları], [hello özgün istemci istek parametrelerinden], ve [hello arka uç yanıt parametrelerinden].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="7b0ff-145">Şu anda, yanıtları değiştirmek için hiçbir portal deneyimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="7b0ff-146">toolearn tooapply proxies.json, bu özellikten nasıl görürüm [responseOverrides nesnesi tanımlayın].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="7b0ff-147"><a name="using-variables"></a>Değişkenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="7b0ff-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="7b0ff-148">bir proxy için başlangıç yapılandırmasını toobe statik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="7b0ff-149">Bu toouse değişkenleri hello ilk istek, hello arka uç yanıt ya da uygulama ayarları koşulu.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="7b0ff-150"><a name="request-parameters"></a>Başvuru İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="7b0ff-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="7b0ff-151">İstek parametreleri toohello arka uç URL'si özelliği girdi olarak veya isteklerin ve yanıtların değiştirerek bir parçası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="7b0ff-152">Bazı parametreler hello temel proxy yapılandırma dosyasında belirtilen hello rota şablondan bağlı olabilir ve diğerleri hello gelen istek özelliklerinden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="7b0ff-153">Rota şablon parametreleri</span><span class="sxs-lookup"><span data-stu-id="7b0ff-153">Route template parameters</span></span>
<span data-ttu-id="7b0ff-154">Merhaba rota şablonda kullanılan parametreler ada göre başvurulan kullanılabilir toobe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="7b0ff-155">Merhaba parametre adı kaşlı ({}) içine alınır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="7b0ff-156">Örneğin, bir proxy gibi bir rota şablonu varsa `/pets/{petId}`, hello arka uç URL'si hello değerini içerebilir `{petId}`, olarak `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="7b0ff-157">Merhaba rota şablonu bir joker karakter olarak gibi kesilip kesilmediğini `/api/{*restOfPath}`, hello değeri `{restOfPath}` hello gelen istek yol bölümlerinin kalan hello dize gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="7b0ff-158">Ek İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="7b0ff-158">Additional request parameters</span></span>
<span data-ttu-id="7b0ff-159">Ayrıca toohello rota şablonu parametreleri, değerleri aşağıdaki hello yapılandırma değerleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="7b0ff-160">**{request.method}** : Merhaba hello özgün istekte kullanılan HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="7b0ff-161">**{request.headers. \<HeaderName\>}**: hello özgün isteğinden okunabilir bir üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="7b0ff-162">Değiştir  *\<HeaderName\>*  tooread istediğiniz hello üstbilgisinin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="7b0ff-163">Merhaba üstbilgi hello isteğinde bulunmuyorsa hello değer hello boş dize olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="7b0ff-164">**{request.querystring. \<ParameterName\>}**: hello özgün isteğinden okunabilir bir sorgu dizesi parametresi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="7b0ff-165">Değiştir  *\<ParameterName\>*  tooread istediğiniz hello parametresinin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="7b0ff-166">Merhaba parametre hello isteğinde bulunmuyorsa hello değer hello boş dize olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="7b0ff-167"><a name="response-parameters"></a>Başvuru arka uç yanıt parametreleri</span><span class="sxs-lookup"><span data-stu-id="7b0ff-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="7b0ff-168">Yanıt parametrelerinin hello yanıt toohello istemci değiştirerek bir parçası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="7b0ff-169">değerleri aşağıdaki hello yapılandırma değerleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="7b0ff-170">**{backend.response.statusCode}** : Merhaba hello arka uç yanıtta döndürülen HTTP durum kodu.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="7b0ff-171">**{backend.response.statusReason}** : hello arka uç yanıtta döndürülen hello HTTP neden ifadesini.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="7b0ff-172">**{backend.response.headers. \<HeaderName\>}**: hello arka uç yanıttan okunabilir bir üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="7b0ff-173">Değiştir  *\<HeaderName\>*  tooread istediğiniz hello üstbilgisinin hello adı.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="7b0ff-174">Merhaba üstbilgi hello isteğinde bulunmuyorsa hello değer hello boş dize olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="7b0ff-175"><a name="use-appsettings"></a>Başvuru uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="7b0ff-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="7b0ff-176">Ayrıca başvurabilir [hello işlev uygulaması için tanımlanan uygulama ayarları](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) hello ayarı adı yüzde işaretleri (%) çevreleyen tarafından.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="7b0ff-177">Örneğin, arka uç URL'sini *https://%ORDER_PROCESSING_HOST%/api/orders* "Merhaba ORDER_PROCESSING_HOST ayarı hello değerle değiştirilen ORDER_PROCESSING_HOST %" olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="7b0ff-178">Birden çok dağıtım varsa, arka uç ana bilgisayarlar için uygulama ayarları kullanın veya test ortamları.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="7b0ff-179">Bu şekilde, her zaman Konuşmayı emin yapabileceğiniz sağ geri toohello end bu ortam için.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="7b0ff-180">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b0ff-180">Advanced configuration</span></span>

<span data-ttu-id="7b0ff-181">yapılandırdığınız hello proxy'leri hello işlevi uygulama dizin kökünde bulunan bir proxies.json dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="7b0ff-182">El ile bu dosyasını düzenleyin ve hello birini kullandığınızda, uygulamanızın bir parçası olarak dağıtmanız [dağıtım yöntemleri](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) bu işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="7b0ff-183">Merhaba özelliği olmalı [etkin](#enable) işlenen hello dosya toobe için.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="7b0ff-184">Bir hello dağıtım yöntemleri ayarlamadıysanız hello portalında hello proxies.json dosyayla çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="7b0ff-185">Git tooyour işlev uygulaması, select **Platform özellikleri**ve ardından **App Service Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="7b0ff-186">Bunu yaparak, hello tüm dosya yapısı işlevi uygulamanızın görüntüleyin ve ardından değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="7b0ff-187">Proxies.JSON adlandırılmış proxy'leri ve tanımlarını oluşan bir proxy nesnesi tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="7b0ff-188">İsteğe bağlı olarak, düzenleyicinizi destekliyorsa, başvurabileceğiniz bir [JSON şeması](http://json.schemastore.org/proxies) için kod tamamlama.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="7b0ff-189">Bir örnek dosyası hello şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-189">An example file might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="7b0ff-190">Her proxy gibi kolay bir ada sahip *proxy1* örnek önceki hello içinde.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="7b0ff-191">Merhaba karşılık gelen proxy tanım nesnesi, aşağıdaki özelliklere hello tarafından tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="7b0ff-192">**matchCondition**:--Bu proxy hello yürütülmesini tetiklemek hello istekleri tanımlayan bir nesne gerekli.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="7b0ff-193">İle paylaşılan iki özellikler içeren [HTTP Tetikleyicileri]:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="7b0ff-194">_yöntemleri_: proxy hello hello HTTP yöntemleri bir dizi yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="7b0ff-195">Belirtilmezse, hello proxy tooall HTTP yöntemleri hello rotada yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="7b0ff-196">_Rota_: gerekli--hangi URL'lerin proxy isteği denetleme hello rota şablonu tanımlar yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="7b0ff-197">Farklı olarak HTTP tetikleyicileri, varsayılan değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="7b0ff-198">**backendUri**: hello arka uç kaynak toowhich hello isteği hello URL'sini yönlendirilirken.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="7b0ff-199">Bu değer, uygulama ayarları ve parametreleri hello özgün istemci isteğinden başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="7b0ff-200">Bu özellik dahil edilmezse, Azure işlevlerinin bir HTTP 200 Tamam ile yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="7b0ff-201">**requestOverrides**: dönüşümleri toohello arka uç isteği tanımlayan bir nesne.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="7b0ff-202">Bkz: [requestOverrides nesnesi tanımlayın].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="7b0ff-203">**responseOverrides**: dönüşümleri toohello istemci yanıt tanımlayan bir nesne.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="7b0ff-204">Bkz: [responseOverrides nesnesi tanımlayın].</span><span class="sxs-lookup"><span data-stu-id="7b0ff-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="7b0ff-205">Merhaba rota Özelliği Azure işlevleri proxy'leri hello işlevleri ana bilgisayar yapılandırmasının hello routeprefix öğesi özelliğini dikkate almaz.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="7b0ff-206">Tooinclude /api gibi bir önek istiyorsanız hello rota özelliğinde eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="7b0ff-207"><a name="requestOverrides"></a>RequestOverrides nesnesi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="7b0ff-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="7b0ff-208">Merhaba requestOverrides nesnesi hello arka uç kaynak çağrıldığında toohello istek yapılan değişiklikleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="7b0ff-209">Merhaba nesne hello aşağıdaki özelliklere göre tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="7b0ff-210">**backend.Request.Method**: Merhaba toocall hello arka uç kullanılan HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="7b0ff-211">**backend.Request.QueryString. \<ParameterName\>**: hello çağrısı toohello arka uç için ayarlanabilir bir sorgu dizesi parametresi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="7b0ff-212">Değiştir  *\<ParameterName\>*  tooset istediğiniz hello parametresinin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="7b0ff-213">Merhaba boş dize sağlanırsa, hello parametre hello arka uç isteği dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="7b0ff-214">**backend.Request.Headers. \<HeaderName\>**: hello çağrısı toohello arka uç için ayarlanabilecek üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="7b0ff-215">Değiştir  *\<HeaderName\>*  tooset istediğiniz hello üstbilgisinin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="7b0ff-216">Merhaba boş dize sağlarsanız, hello üstbilgi hello arka uç isteği dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="7b0ff-217">Uygulama ayarları ve parametreleri değerleri hello özgün istemci isteğinden başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="7b0ff-218">Örnek bir yapılandırma hello şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-218">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="7b0ff-219"><a name="responseOverrides"></a>ResponseOverrides nesnesi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="7b0ff-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="7b0ff-220">Merhaba requestOverrides nesnesi geri toohello istemci geçti toohello yanıt yapılan değişiklikleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="7b0ff-221">Merhaba nesne hello aşağıdaki özelliklere göre tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="7b0ff-222">**response.statusCode**: hello HTTP durum kodu toobe toohello istemci döndürdü.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="7b0ff-223">**response.statusReason**: hello HTTP neden tümcecik toobe toohello istemci döndürdü.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="7b0ff-224">**Response.body**: hello gövde toobe hello dize gösterimini toohello istemci döndürdü.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="7b0ff-225">**Response.Headers. \<HeaderName\>**: hello yanıt toohello istemci için ayarlanabilecek üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="7b0ff-226">Değiştir  *\<HeaderName\>*  tooset istediğiniz hello üstbilgisinin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="7b0ff-227">Merhaba boş dize sağlarsanız, hello üstbilgi hello yanıtta dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="7b0ff-228">Uygulama ayarları, hello özgün istemci istek parametrelerinden ve parametreleri değerleri hello arka uç yanıttan başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="7b0ff-229">Örnek bir yapılandırma hello şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="7b0ff-229">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="7b0ff-230">Bu örnekte, hello gövde doğrudan, bu nedenle Hayır ayarlı `backendUri` özelliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="7b0ff-231">Merhaba örnek API'leri mocking için Azure işlevleri proxy'leri nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b0ff-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[Azure portal]: https://portal.azure.com
[HTTP Tetikleyicileri]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[requestOverrides nesnesi tanımlayın]: #requestOverrides
[responseOverrides nesnesi tanımlayın]: #responseOverrides
[uygulama ayarları]: #use-appsettings
[değişkenlerini kullanın]: #using-variables
[hello özgün istemci istek parametrelerinden]: #request-parameters
[hello arka uç yanıt parametrelerinden]: #response-parameters
