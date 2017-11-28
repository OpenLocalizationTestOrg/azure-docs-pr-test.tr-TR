---
title: aaaUsing API Management hizmet toogenerate HTTP istekleri
description: "API Management toocall dış Hizmetleri, API toouse istek ve yanıt ilkeleri öğrenin"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="b6f9b-103">Dış Hizmetleri'nden hello Azure API Management hizmeti kullanma</span><span class="sxs-lookup"><span data-stu-id="b6f9b-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="b6f9b-104">Merhaba ilkelerini Azure API Management hizmeti içinde çok çeşitli tamamen hello gelen istek, hello giden yanıt ve temel yapılandırma bilgileri göre yararlı iş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="b6f9b-105">Ancak, API Management dış hizmetler ile mümkün toointeract olan ilkeleri açılır pek çok daha fazla fırsatı.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="b6f9b-106">Biz biz hello ile nasıl etkileşim daha önce gördünüz [günlüğe kaydetme, izleme ve analiz için Azure olay hub'ı hizmeti](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="b6f9b-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="b6f9b-107">Bu makaledeki tüm dış HTTP ile toointeract izin ilkeleri hizmet tabanlı gösterecek.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="b6f9b-108">Bu ilkeler, kullanılan toomanipulate hello özgün istek ve yanıt şekilde olacak bilgileri almak için veya uzak olaylarını tetiklemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="b6f9b-109">Bir şekilde İsteği Gönder</span><span class="sxs-lookup"><span data-stu-id="b6f9b-109">Send-One-Way-Request</span></span>
<span data-ttu-id="b6f9b-110">Büyük olasılıkla hello basit dış etkileşim hello yangın ve unut stil bazı önemli olay türünü bildirim bir dış hizmet toobe sağlayan isteğinin gelir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="b6f9b-111">Merhaba denetim akışı İlkesi kullanırız `choose` her türlü ilginizi çekiyor mu ve daha sonra Merhaba, koşul koşulu karşılandığında, biz hello kullanarak harici bir HTTP isteği yapabilir toodetect [bir şekilde İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="b6f9b-112">Bu ileti sistemi Hipchat veya boşluk ya da posta API SendGrid veya MailChimp gibi gibi bir isteği tooa olabilir veya kritik destek olaylar için şuna benzer PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="b6f9b-113">Bu ileti sistemlerini biz kolayca çağırabileceği basit HTTP API'ler sahip.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="b6f9b-114">Kayma ile uyarı</span><span class="sxs-lookup"><span data-stu-id="b6f9b-114">Alerting with Slack</span></span>
<span data-ttu-id="b6f9b-115">Aşağıdaki örnek hello nasıl toosend ileti tooa hello HTTP yanıtı durum kodu daha büyükse, sohbet odası boşluk veya too500 eşit gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="b6f9b-116">Bizim API İstemci hello bizim arka uç API'si sorun kendilerini çözümlenemiyor bir 500 aralığı hatasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="b6f9b-117">Genellikle, bazı tür bir araya bizim bölümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="b6f9b-118">Kayma gelen web kancaları hello kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="b6f9b-119">Gelen web kancası yapılandırırken kayma hello Slack kanal toodo basit bir POST isteği ve toopass bir ileti sağlayan özel bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="b6f9b-120">Merhaba oluşturuyoruz JSON gövdesi kayma tarafından tanımlanan bir biçimini temel alır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Slack Web kancası](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="b6f9b-122">Yangın uyguluyor ve yeterli unuttunuz mu?</span><span class="sxs-lookup"><span data-stu-id="b6f9b-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="b6f9b-123">İstek yangın ve unut stili kullanırken belirli bileşim yoktur.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="b6f9b-124">Herhangi bir nedenle olduğu varsa, hello isteği başarısız olur ve ardından hello hatası raporlanmayacak.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="b6f9b-125">Bu belirli durumda hello karmaşıklığını ikincil hata raporlama sistemi ve hello yanıtı bekleniyor hello ek performans maliyeti olması garanti değil.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="b6f9b-126">Temel toocheck hello yanıt olduğu senaryolar için sonra hello [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) ilkedir daha iyi bir seçenek.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="b6f9b-127">Gönderme isteği</span><span class="sxs-lookup"><span data-stu-id="b6f9b-127">Send-Request</span></span>
<span data-ttu-id="b6f9b-128">Merhaba `send-request` işleme işlevleri ve daha fazla ilke işleme için kullanılan dönüş verileri toohello API management hizmeti karmaşık bir dış hizmet tooperform kullanarak ilke etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="b6f9b-129">Başvuru belirteçleri yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="b6f9b-129">Authorizing reference tokens</span></span>
<span data-ttu-id="b6f9b-130">API Management ana işlevinin arka uç kaynaklarına koruyor.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="b6f9b-131">API tarafından kullanılan hello yetkilendirme sunucusu oluşturursa [JWT belirteçleri](http://jwt.io/) , OAuth2 akışının parçası olarak olarak [Azure Active Directory](../active-directory/active-directory-aadconnect.md) mu hello kullanabilirsiniz `validate-jwt` İlkesi tooverify hello geçerliliğini Merhaba belirteci.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="b6f9b-132">Ancak, bazı yetkilendirme sunucuları ne denir oluşturma [başvuru belirteçleri](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) , doğrulanamıyor çağrı geri toohello yetkilendirme sunucusu yapmadan.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="b6f9b-133">Standartlaştırılmış introspection</span><span class="sxs-lookup"><span data-stu-id="b6f9b-133">Standardized introspection</span></span>
<span data-ttu-id="b6f9b-134">Hello geçmiş başvuru belirteci yetkilendirme sunucusu ile doğrulama standartlaştırılmış hiçbir şekilde açıldı.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="b6f9b-135">Ancak en son önerilen standart [RFC 7662](https://tools.ietf.org/html/rfc7662) hello kaynak sunucuda bir belirteç hello geçerliliğini nasıl doğrulayabilirsiniz tanımlar IETF tarafından yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="b6f9b-136">Merhaba belirteci ayıklanıyor</span><span class="sxs-lookup"><span data-stu-id="b6f9b-136">Extracting hello token</span></span>
<span data-ttu-id="b6f9b-137">Merhaba ilk tooextract hello hello Authorization Üstbilgisi belirtecinden adımdır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="b6f9b-138">Merhaba üstbilgi değeri ile Merhaba biçimlendirilmiş `Bearer` Yetkilendirme düzeni, tek bir boşluk ve ardından hello yetkilendirme belirteci olarak başına [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="b6f9b-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="b6f9b-139">Ne yazık ki burada hello Yetkilendirme düzeni atlanmış durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="b6f9b-140">Bu tooaccount ayrıştırılırken, biz hello üstbilgi değeri bir boşluk ve select hello son dizisini döndürülen hello dizeden bölün.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="b6f9b-141">Bu, hatalı biçimlendirilmiş yetkilendirme üstbilgileri için geçici bir çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="b6f9b-142">Merhaba doğrulama isteği yapan</span><span class="sxs-lookup"><span data-stu-id="b6f9b-142">Making hello validation request</span></span>
<span data-ttu-id="b6f9b-143">Biz hello yetkilendirme belirtecini olduktan sonra biz hello isteği toovalidate hello belirteci yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="b6f9b-144">RFC 7662 bu işlem introspection çağırır ve gerektiren, `POST` bir HTML form toohello introspection kaynak.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="b6f9b-145">Merhaba HTML formu en az olarak hello anahtarla bir anahtar/değer çifti içermelidir `token`.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="b6f9b-146">Bu istek toohello yetkilendirme sunucusu ayrıca kötü amaçlı istemciler için geçerli belirteçleri trawling Git olamaz kimliği doğrulanmış tooensure olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a><span data-ttu-id="b6f9b-147">Merhaba yanıt denetleniyor</span><span class="sxs-lookup"><span data-stu-id="b6f9b-147">Checking hello response</span></span>
<span data-ttu-id="b6f9b-148">Merhaba `response-variable-name` özniteliktir kullanılan toogive erişim hello yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="b6f9b-149">Merhaba bu özelliği içinde tanımlı adı bir anahtar olarak hello kullanılabilir `context.Variables` sözlük tooaccess hello `IResponse` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="b6f9b-150">Merhaba yanıt nesnesinden biz hello gövde alabilir ve RFC 7622 söyler, bize, hello yanıt bir JSON nesnesi olmalıdır ve adlı en az bir özellik içermelidir `active` diğer bir deyişle bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="b6f9b-151">Zaman `active` hello belirteci geçerli kabul doğrudur.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="b6f9b-152">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="b6f9b-152">Reporting failure</span></span>
<span data-ttu-id="b6f9b-153">Kullandığımız bir `<choose>` İlkesi toodetect hello belirteci geçersiz varsa ve bu durumda, bir 401 yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="b6f9b-154">Göre [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) açıklayan nasıl `bearer` belirteçleri kullanılması gerekir, ayrıca döndürürüz bir `WWW-Authenticate` hello 401 yanıt üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="b6f9b-155">Merhaba WWW-Authenticate olduğu hedeflenen tooinstruct nasıl bir istemcide tooconstruct düzgün yetkili isteği.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="b6f9b-156">Toohello çeşitli yaklaşımlar hello OAuth2 framework ile olası, zor olduğu tüm hello toocommunicate gerekli bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="b6f9b-157">Neyse ki vardır çaba devam toohelp [istemcileri bulmak nasıl tooproperly yetkilendirmek istekleri tooa kaynak sunucusu](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="b6f9b-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="b6f9b-158">Son çözüm</span><span class="sxs-lookup"><span data-stu-id="b6f9b-158">Final solution</span></span>
<span data-ttu-id="b6f9b-159">Tüm hello parçaları bir araya getirilmesi, biz ilke aşağıdaki hello alın:</span><span class="sxs-lookup"><span data-stu-id="b6f9b-159">Putting all hello pieces together, we get hello following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="b6f9b-160">Bu yalnızca nasıl birçok örnekleri biridir hello `send-request` İlkesi kullanılan toointegrate yararlı dış hizmetler isteklerin ve yanıtların hello API Management hizmet akan hello işlemine olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="b6f9b-161">Yanıt oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6f9b-161">Response Composition</span></span>
<span data-ttu-id="b6f9b-162">Merhaba `send-request` İlkesi hello önceki örnekte gördüğümüz veya tam değiştirme için hello arka uç arama kullanılan bir birincil istek tooa arka uç sistemi geliştirme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="b6f9b-163">Bu teknik kullanılarak kolayca toplanır bileşik kaynakları birden çok farklı sistemlerden oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="b6f9b-164">Bir pano oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6f9b-164">Building a dashboard</span></span>
<span data-ttu-id="b6f9b-165">Bazen birden fazla arka uç sistemlerinde bulunan toobe mümkün tooexpose bilgilerini örneğin, bir Pano toodrive istersiniz.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="b6f9b-166">Merhaba KPI'leri gelen tüm farklı arka uçları, ancak tooprovide doğrudan erişim toothem tercih ediyorsanız ve tek bir istekte tüm hello bilgisi alınamadı, iyi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="b6f9b-167">Belki de hello arka uç bilgilerin bazıları gereken bazı dilimleme ve sağlanır ve biraz önce temizleme!</span><span class="sxs-lookup"><span data-stu-id="b6f9b-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="b6f9b-168">Bileşik kaynak yararlı tooreduce olacaktır mümkün toocache olan hello arka uç yük kendi underperforming ölçümleri değiştirirseniz, sipariş toosee hello F5 anahtar sözcüğüne alýþkanlýk kullanıcınız bildiğiniz gibi.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="b6f9b-169">Merhaba kaynak faking</span><span class="sxs-lookup"><span data-stu-id="b6f9b-169">Faking hello resource</span></span>
<span data-ttu-id="b6f9b-170">İlk adım toobuilding hello tooconfigure hello API Management yayımcı portalına yeni bir işlemde bizim Pano kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="b6f9b-171">Bu yer tutucu kullanılan işleminin tooconfigure bizim birleşim İlkesi toobuild olacaktır bizim dinamik kaynak.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Pano işlemi](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="b6f9b-173">Merhaba istekleri yapan</span><span class="sxs-lookup"><span data-stu-id="b6f9b-173">Making hello requests</span></span>
<span data-ttu-id="b6f9b-174">Bir kez hello `dashboard` işlemi oluşturulan biz özel olarak bu işlem için bir ilke yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Pano işlemi](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="b6f9b-176">Merhaba ilk adımı biz tooour arka uç iletebilir hello gelen istek, herhangi bir sorgu parametre tooextract aynıdır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="b6f9b-177">Bu örnekte bir zaman aralığında bağlı bilgileri bizim Pano gösteren bir nedenle sahip bir `fromDate` ve `toDate` parametresi.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="b6f9b-178">Merhaba kullanırız `set-variable` ilke tooextract hello bilgilerini hello istek URL'si.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="b6f9b-179">Biz bu bilgileri olduktan sonra istekleri tooall hello arka uç sistemleri yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="b6f9b-180">Her istek hello parametre bilgilerini içeren yeni bir URL oluşturur ve ilgili sunucusuna çağırır ve hello yanıt içeriği değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="b6f9b-181">Bu istekler ideal olmayan sırayla çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="b6f9b-182">Gelecek bir sürümde biz adlı yeni bir ilke size sunmuş olacağız `wait` bu istekleri tooexecute paralel olarak etkinleştirecek.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="b6f9b-183">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b6f9b-183">Responding</span></span>
<span data-ttu-id="b6f9b-184">tooconstruct hello bileşik yanıt hello kullanabileceğiniz [return yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="b6f9b-185">Merhaba `set-body` öğesi, bir ifade tooconstruct kullanabilir yeni `JObject` özellikleri olarak katıştırılmış tüm hello bileşen Beyanları ile.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="b6f9b-186">Merhaba tam İlkesi şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="b6f9b-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="b6f9b-187">Bunu hala yeterince etkili olacaktır güncel değil, bir saat olsa bile anlamına hello veri hello yapısını anlamak için biz yapılandırabilirsiniz hello yer tutucu işlemi hello yapılandırmasında hello Pano kaynak toobe için en az bir saat önbelleğe alınan tooconvey değerli bilgiler toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="b6f9b-188">Özet</span><span class="sxs-lookup"><span data-stu-id="b6f9b-188">Summary</span></span>
<span data-ttu-id="b6f9b-189">Azure API Management hizmeti, seçmeli olarak olabilir esnek ilkeler tooHTTP trafiği uygulanan sağlar ve arka uç hizmetlerinin birleşim etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="b6f9b-190">Uyarı İşlevler, doğrulama, doğrulama yetenekleri ile API ağ geçidi tooenhance istediğiniz ya da birden fazla arka uç hizmetlerini temel alarak yeni bileşik kaynakları oluşturmak isteyip hello `send-request` ve ilgili ilkeler olanaklar dünyası açın.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="b6f9b-191">Bu ilkelerin video genel izleyin</span><span class="sxs-lookup"><span data-stu-id="b6f9b-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="b6f9b-192">Merhaba hakkında daha fazla bilgi için [bir şekilde İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), ve [return yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) bu makalede ele alınan ilkeleri Lütfen video aşağıdaki hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="b6f9b-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

