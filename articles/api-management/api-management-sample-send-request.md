---
title: "HTTP istekleri oluşturmak için API Management hizmeti kullanma"
description: "Dış hizmetler, API çağrısı için API Management'te istek ve yanıt ilkeleri kullanma hakkında bilgi edinin"
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="629fa-103">Azure API Management hizmetinden dış hizmetler kullanarak</span><span class="sxs-lookup"><span data-stu-id="629fa-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="629fa-104">Azure API Management hizmetinde kullanılabilir ilkeler çeşitli yararlı iş tamamen gelen istek, giden yanıt ve temel yapılandırma bilgileri göre yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="629fa-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="629fa-105">Ancak, dış API Management hizmetlerinden etkileşimde yapamamasına ilkeleri açılır pek çok daha fazla fırsatı.</span><span class="sxs-lookup"><span data-stu-id="629fa-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="629fa-106">Biz nasıl biz etkileşim kurabildikleri daha önce gördünüz [günlüğe kaydetme, izleme ve analiz için Azure olay hub'ı hizmeti](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="629fa-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="629fa-107">Bu makalede, tüm dış HTTP ile etkileşim kurmasına izin ilkeleri hizmet tabanlı gösterecek.</span><span class="sxs-lookup"><span data-stu-id="629fa-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="629fa-108">Bu ilkeler, uzak olaylarını tetiklemek veya özgün istek ve yanıt bir şekilde işlemek için kullanılan bilgileri almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="629fa-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="629fa-109">Bir şekilde İsteği Gönder</span><span class="sxs-lookup"><span data-stu-id="629fa-109">Send-One-Way-Request</span></span>
<span data-ttu-id="629fa-110">Büyük olasılıkla önemli olay çeşit bildirim almak bir dış hizmet veren istek yangın ve unut stilini basit dış etkileşim olduğu.</span><span class="sxs-lookup"><span data-stu-id="629fa-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="629fa-111">Denetim akışı İlkesi kullanırız `choose` biz ilgilendiğiniz ve Koşul sağlanıyorsa, daha sonra biz dış bir HTTP isteği kullanarak yapabilirsiniz koşulu her türlü algılamak için [bir şekilde İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="629fa-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="629fa-112">Bu ileti sistemi Hipchat veya boşluk ya da posta API SendGrid veya MailChimp gibi gibi bir istek olabilir veya kritik destek olaylar için şuna benzer PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="629fa-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="629fa-113">Bu ileti sistemlerini biz kolayca çağırabileceği basit HTTP API'ler sahip.</span><span class="sxs-lookup"><span data-stu-id="629fa-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="629fa-114">Kayma ile uyarı</span><span class="sxs-lookup"><span data-stu-id="629fa-114">Alerting with Slack</span></span>
<span data-ttu-id="629fa-115">Aşağıdaki örnek, HTTP yanıtı durum kodu 500 eşit veya daha büyük ise Slack sohbet odasına bir ileti göndermek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="629fa-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="629fa-116">500 aralık hatası API'mize istemci kendilerini çözümlenemiyor bizim arka uç API'si bir sorun olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="629fa-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="629fa-117">Genellikle, bazı tür bir araya bizim bölümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="629fa-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="629fa-118">Kayma gelen web kancaları kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="629fa-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="629fa-119">Gelen web kancası yapılandırırken, boşluk, basit bir POST isteği yapmak için ve bir ileti Slack kanal geçmesine izin veren özel bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="629fa-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="629fa-120">Oluşturuyoruz JSON gövdesi kayma tarafından tanımlanan bir biçimini temel alır.</span><span class="sxs-lookup"><span data-stu-id="629fa-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Slack Web kancası](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="629fa-122">Yangın uyguluyor ve yeterli unuttunuz mu?</span><span class="sxs-lookup"><span data-stu-id="629fa-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="629fa-123">İstek yangın ve unut stili kullanırken belirli bileşim yoktur.</span><span class="sxs-lookup"><span data-stu-id="629fa-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="629fa-124">Herhangi bir nedenle olduğu varsa, istek başarısız olur ve ardından hata raporlanmayacak.</span><span class="sxs-lookup"><span data-stu-id="629fa-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="629fa-125">Bu belirli bir durumda, sistem ve yanıt bekleme ek performans maliyeti raporlama ikincil bir hataya neden karmaşıklığını garanti değil.</span><span class="sxs-lookup"><span data-stu-id="629fa-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="629fa-126">Yanıt denetlemek için gerekli olduğu senaryolar için sonra [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) ilkedir daha iyi bir seçenek.</span><span class="sxs-lookup"><span data-stu-id="629fa-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="629fa-127">Gönderme isteği</span><span class="sxs-lookup"><span data-stu-id="629fa-127">Send-Request</span></span>
<span data-ttu-id="629fa-128">`send-request` İlkesi etkinleştirir karmaşık işleme işlevleri gerçekleştirmek ve veri API Management hizmeti dönmek için bir dış hizmet kullanarak daha fazla ilke işleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="629fa-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="629fa-129">Başvuru belirteçleri yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="629fa-129">Authorizing reference tokens</span></span>
<span data-ttu-id="629fa-130">API Management ana işlevinin arka uç kaynaklarına koruyor.</span><span class="sxs-lookup"><span data-stu-id="629fa-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="629fa-131">API tarafından kullanılan yetkilendirme sunucusu oluşturursa [JWT belirteçleri](http://jwt.io/) kendi OAuth2 akışının parçası olarak olarak [Azure Active Directory](../active-directory/active-directory-aadconnect.md) mu kullanabileceğiniz sonra `validate-jwt` İlkesi belirtecin geçerliliğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="629fa-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="629fa-132">Ancak, bazı yetkilendirme sunucuları ne denir oluşturma [başvuru belirteçleri](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) , doğrulanamıyor yetkilendirme sunucuya geri arama yapmadan.</span><span class="sxs-lookup"><span data-stu-id="629fa-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="629fa-133">Standartlaştırılmış introspection</span><span class="sxs-lookup"><span data-stu-id="629fa-133">Standardized introspection</span></span>
<span data-ttu-id="629fa-134">Geçmişte başvuru belirteci yetkilendirme sunucusu ile doğrulama hiçbir standartlaştırılmış şekilde açıldı.</span><span class="sxs-lookup"><span data-stu-id="629fa-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="629fa-135">Ancak en son önerilen standart [RFC 7662](https://tools.ietf.org/html/rfc7662) bir kaynak sunucuda bir belirtecin geçerliliğini nasıl doğrulayabilirsiniz tanımlar IETF tarafından yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="629fa-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="629fa-136">Belirteç ayıklanıyor</span><span class="sxs-lookup"><span data-stu-id="629fa-136">Extracting the token</span></span>
<span data-ttu-id="629fa-137">Belirteç yetkilendirme başlığından ayıklamak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="629fa-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="629fa-138">Üstbilgi değeri ile biçimlendirilmiş olması `Bearer` Yetkilendirme düzeni, tek bir boşluk ve ardından yetkilendirme belirteci olarak başına [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="629fa-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="629fa-139">Ne yazık ki burada Yetkilendirme düzeni atlanmış durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="629fa-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="629fa-140">Ayrıştırılırken bu hesap için bir alanı üstbilgi değeri Böl ve son dize dizeleri döndürülen diziden seçin.</span><span class="sxs-lookup"><span data-stu-id="629fa-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="629fa-141">Bu, hatalı biçimlendirilmiş yetkilendirme üstbilgileri için geçici bir çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="629fa-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="629fa-142">Doğrulama isteği yapan</span><span class="sxs-lookup"><span data-stu-id="629fa-142">Making the validation request</span></span>
<span data-ttu-id="629fa-143">Biz yetkilendirme belirtecini olduktan sonra biz belirteci doğrulama isteği yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="629fa-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="629fa-144">RFC 7662 bu işlem introspection çağırır ve gerektiren, `POST` introspection kaynak için bir HTML formu.</span><span class="sxs-lookup"><span data-stu-id="629fa-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="629fa-145">HTML formu anahtarla en az bir anahtar/değer çifti içermelidir `token`.</span><span class="sxs-lookup"><span data-stu-id="629fa-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="629fa-146">Kötü amaçlı istemciler için geçerli belirteçleri trawling Git olamaz emin olmak için bu istek için yetkilendirme sunucusu da kimliğinin doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="629fa-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="629fa-147">Yanıt denetleniyor</span><span class="sxs-lookup"><span data-stu-id="629fa-147">Checking the response</span></span>
<span data-ttu-id="629fa-148">`response-variable-name` Özniteliği döndürülen yanıt erişmesini sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="629fa-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="629fa-149">Bu özelliği içinde tanımlı adı bir anahtar olarak kullanılan `context.Variables` erişmek için sözlük `IResponse` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="629fa-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="629fa-150">Yanıt nesnesinden biz gövdesi alabilir ve RFC 7622 söyler, bize, yanıt bir JSON nesnesi olmalıdır ve adlı en az bir özellik içermelidir `active` diğer bir deyişle bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="629fa-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="629fa-151">Zaman `active` belirtecin geçerli kabul doğrudur.</span><span class="sxs-lookup"><span data-stu-id="629fa-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="629fa-152">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="629fa-152">Reporting failure</span></span>
<span data-ttu-id="629fa-153">Kullandığımız bir `<choose>` belirteci geçersiz varsa ve bu durumda, algılamak için ilke 401 yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="629fa-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="629fa-154">Göre [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) açıklayan nasıl `bearer` belirteçleri kullanılması gerekir, ayrıca döndürürüz bir `WWW-Authenticate` 401 yanıt üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="629fa-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="629fa-155">WWW-Authenticate amaçlanmıştır düzgün yetkili isteği oluşturmak nasıl bir istemcide istemek üzere.</span><span class="sxs-lookup"><span data-stu-id="629fa-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="629fa-156">Çeşitli yaklaşımlar OAuth2 framework ile olası nedeni, gerekli tüm bilgileri iletişim kurmak zordur.</span><span class="sxs-lookup"><span data-stu-id="629fa-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="629fa-157">Neyse ki devam yardımcı olmak üzere çabalarına vardır [istemcileri bulmak düzgün bir şekilde bir kaynak sunucuya isteklerini yetkilendirmek nasıl](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="629fa-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="629fa-158">Son çözüm</span><span class="sxs-lookup"><span data-stu-id="629fa-158">Final solution</span></span>
<span data-ttu-id="629fa-159">Tüm parçaları bir araya getirilmesi, biz aşağıdaki İlkesi alın:</span><span class="sxs-lookup"><span data-stu-id="629fa-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="629fa-160">Bu yalnızca, birçok örnekleri nasıl biri `send-request` İlkesi, isteklerin ve yanıtların API Management hizmet aracılığıyla akan işlemine yararlı dış hizmetler tümleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="629fa-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="629fa-161">Yanıt oluşturma</span><span class="sxs-lookup"><span data-stu-id="629fa-161">Response Composition</span></span>
<span data-ttu-id="629fa-162">`send-request` İlkesi, önceki örnekte gördüğümüz veya tam değiştirme için arka uç çağrının kullanılabilmesi için bir arka uç sistemi birincil isteğine geliştirme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="629fa-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="629fa-163">Bu teknik kullanılarak kolayca toplanır bileşik kaynakları birden çok farklı sistemlerden oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="629fa-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="629fa-164">Bir pano oluşturma</span><span class="sxs-lookup"><span data-stu-id="629fa-164">Building a dashboard</span></span>
<span data-ttu-id="629fa-165">Bazen birden fazla arka uç sistemlerinde, örneğin bulunan bilgilerini kullanıma sunmak için bir Pano sürücüsüne kullanabilmek ister.</span><span class="sxs-lookup"><span data-stu-id="629fa-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="629fa-166">Tüm farklı arka uçları, KPI'ları gelir ancak bunları doğrudan erişim sağlamak için değil tercih ve tüm bilgileri tek bir istekte alınamadı, iyi olur.</span><span class="sxs-lookup"><span data-stu-id="629fa-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="629fa-167">Belki de arka uç bilgilerin bazıları gereken bazı dilimleme ve sağlanır ve biraz önce temizleme!</span><span class="sxs-lookup"><span data-stu-id="629fa-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="629fa-168">Bileşik bu kaynağın önbelleğe yapamamasına kendi underperforming ölçümleri değişebilir olmadığını görmek için F5 tuşuna sözcüğüne, alýþkanlýk kullanıcınız bildiğiniz gibi arka uç yükü azaltmak bir yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="629fa-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="629fa-169">Kaynak faking</span><span class="sxs-lookup"><span data-stu-id="629fa-169">Faking the resource</span></span>
<span data-ttu-id="629fa-170">Bizim Pano kaynak oluşturmanın ilk adımı, API Management yayımcı Portalı'nda yeni işlem yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="629fa-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="629fa-171">Bu bizim dinamik kaynak oluşturmak için birleşim ilkemizi yapılandırmak için kullanılan bir yer tutucu işlemi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="629fa-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Pano işlemi](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="629fa-173">İsteği gerçekleştiren</span><span class="sxs-lookup"><span data-stu-id="629fa-173">Making the requests</span></span>
<span data-ttu-id="629fa-174">Bir kez `dashboard` işlemi oluşturulan biz özel olarak bu işlem için bir ilke yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="629fa-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Pano işlemi](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="629fa-176">Böylece biz bunları bizim arka uç için iletme ilk gelen istekte, sorgu parametreleri ayıklamak için adımdır.</span><span class="sxs-lookup"><span data-stu-id="629fa-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="629fa-177">Bu örnekte bir zaman aralığında bağlı bilgileri bizim Pano gösteren bir nedenle sahip bir `fromDate` ve `toDate` parametresi.</span><span class="sxs-lookup"><span data-stu-id="629fa-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="629fa-178">Biz kullanabilirsiniz `set-variable` isteği URL'den bilgi ayıklamak için ilke.</span><span class="sxs-lookup"><span data-stu-id="629fa-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="629fa-179">Biz bu bilgileri olduktan sonra istekleri için tüm arka uç sistemleri yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="629fa-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="629fa-180">Her istek parametre bilgileri içeren yeni bir URL oluşturur ve ilgili sunucusuna çağırır ve yanıt içeriği değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="629fa-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="629fa-181">Bu istekler ideal olmayan sırayla çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="629fa-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="629fa-182">Gelecek bir sürümde biz adlı yeni bir ilke size sunmuş olacağız `wait` paralel olarak çalıştırmak için bu istekleri etkinleştirecek.</span><span class="sxs-lookup"><span data-stu-id="629fa-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="629fa-183">Yanıt</span><span class="sxs-lookup"><span data-stu-id="629fa-183">Responding</span></span>
<span data-ttu-id="629fa-184">Kullanabileceğiniz bileşik yanıt oluşturmak için [return yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="629fa-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="629fa-185">`set-body` Öğesi, yeni bir oluşturmak için bir ifade kullanabilir `JObject` özellikleri olarak katıştırılmış tüm bileşen Beyanları ile.</span><span class="sxs-lookup"><span data-stu-id="629fa-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="629fa-186">Tam İlkesi şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="629fa-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="629fa-187">Bunu hala kullanıcılara değerli bilgiler iletmek için yeterince etkili olacaktır güncel değil, bir saat olsa bile yer tutucu yapılandırmasında biz verilerin yapısını anlamak için en az bir saat için önbelleğe alınacak Pano kaynak yapılandırabilirsiniz işlemi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="629fa-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="629fa-188">Özet</span><span class="sxs-lookup"><span data-stu-id="629fa-188">Summary</span></span>
<span data-ttu-id="629fa-189">Azure API Management hizmeti, HTTP trafiği için seçmeli olarak uygulanabilir esnek ilkeler sağlar ve arka uç hizmetlerinin birleşim etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="629fa-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="629fa-190">Uyarı İşlevler, doğrulama, doğrulama yetenekleri ile API ağ geçidi geliştirmek veya birden fazla arka uç hizmetlerini temel alarak yeni bileşik kaynakları oluşturmak isteyip istemediğinizi `send-request` ve ilgili ilkeler olanaklar dünyası açın.</span><span class="sxs-lookup"><span data-stu-id="629fa-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="629fa-191">Bu ilkelerin video genel izleyin</span><span class="sxs-lookup"><span data-stu-id="629fa-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="629fa-192">Daha fazla bilgi için [bir şekilde İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), ve [return yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) bu makalede ele alınan ilkeleri Lütfen aşağıdaki videoyu izleyin.</span><span class="sxs-lookup"><span data-stu-id="629fa-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

