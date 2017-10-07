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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Dış Hizmetleri'nden hello Azure API Management hizmeti kullanma
Merhaba ilkelerini Azure API Management hizmeti içinde çok çeşitli tamamen hello gelen istek, hello giden yanıt ve temel yapılandırma bilgileri göre yararlı iş yapabilirsiniz. Ancak, API Management dış hizmetler ile mümkün toointeract olan ilkeleri açılır pek çok daha fazla fırsatı.

Biz biz hello ile nasıl etkileşim daha önce gördünüz [günlüğe kaydetme, izleme ve analiz için Azure olay hub'ı hizmeti](api-management-log-to-eventhub-sample.md). Bu makaledeki tüm dış HTTP ile toointeract izin ilkeleri hizmet tabanlı gösterecek. Bu ilkeler, kullanılan toomanipulate hello özgün istek ve yanıt şekilde olacak bilgileri almak için veya uzak olaylarını tetiklemek için kullanılabilir.

## <a name="send-one-way-request"></a>Bir şekilde İsteği Gönder
Büyük olasılıkla hello basit dış etkileşim hello yangın ve unut stil bazı önemli olay türünü bildirim bir dış hizmet toobe sağlayan isteğinin gelir. Merhaba denetim akışı İlkesi kullanırız `choose` her türlü ilginizi çekiyor mu ve daha sonra Merhaba, koşul koşulu karşılandığında, biz hello kullanarak harici bir HTTP isteği yapabilir toodetect [bir şekilde İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) ilkesi. Bu ileti sistemi Hipchat veya boşluk ya da posta API SendGrid veya MailChimp gibi gibi bir isteği tooa olabilir veya kritik destek olaylar için şuna benzer PagerDuty. Bu ileti sistemlerini biz kolayca çağırabileceği basit HTTP API'ler sahip.

### <a name="alerting-with-slack"></a>Kayma ile uyarı
Aşağıdaki örnek hello nasıl toosend ileti tooa hello HTTP yanıtı durum kodu daha büyükse, sohbet odası boşluk veya too500 eşit gösterir. Bizim API İstemci hello bizim arka uç API'si sorun kendilerini çözümlenemiyor bir 500 aralığı hatasını gösterir. Genellikle, bazı tür bir araya bizim bölümü gerektirir.  

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

Kayma gelen web kancaları hello kavramı vardır. Gelen web kancası yapılandırırken kayma hello Slack kanal toodo basit bir POST isteği ve toopass bir ileti sağlayan özel bir URL oluşturur. Merhaba oluşturuyoruz JSON gövdesi kayma tarafından tanımlanan bir biçimini temel alır.

![Slack Web kancası](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>Yangın uyguluyor ve yeterli unuttunuz mu?
İstek yangın ve unut stili kullanırken belirli bileşim yoktur. Herhangi bir nedenle olduğu varsa, hello isteği başarısız olur ve ardından hello hatası raporlanmayacak. Bu belirli durumda hello karmaşıklığını ikincil hata raporlama sistemi ve hello yanıtı bekleniyor hello ek performans maliyeti olması garanti değil. Temel toocheck hello yanıt olduğu senaryolar için sonra hello [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) ilkedir daha iyi bir seçenek.

## <a name="send-request"></a>Gönderme isteği
Merhaba `send-request` işleme işlevleri ve daha fazla ilke işleme için kullanılan dönüş verileri toohello API management hizmeti karmaşık bir dış hizmet tooperform kullanarak ilke etkinleştirir.

### <a name="authorizing-reference-tokens"></a>Başvuru belirteçleri yetkilendirme
API Management ana işlevinin arka uç kaynaklarına koruyor. API tarafından kullanılan hello yetkilendirme sunucusu oluşturursa [JWT belirteçleri](http://jwt.io/) , OAuth2 akışının parçası olarak olarak [Azure Active Directory](../active-directory/active-directory-aadconnect.md) mu hello kullanabilirsiniz `validate-jwt` İlkesi tooverify hello geçerliliğini Merhaba belirteci. Ancak, bazı yetkilendirme sunucuları ne denir oluşturma [başvuru belirteçleri](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) , doğrulanamıyor çağrı geri toohello yetkilendirme sunucusu yapmadan.

### <a name="standardized-introspection"></a>Standartlaştırılmış introspection
Hello geçmiş başvuru belirteci yetkilendirme sunucusu ile doğrulama standartlaştırılmış hiçbir şekilde açıldı. Ancak en son önerilen standart [RFC 7662](https://tools.ietf.org/html/rfc7662) hello kaynak sunucuda bir belirteç hello geçerliliğini nasıl doğrulayabilirsiniz tanımlar IETF tarafından yayımlandı.

### <a name="extracting-hello-token"></a>Merhaba belirteci ayıklanıyor
Merhaba ilk tooextract hello hello Authorization Üstbilgisi belirtecinden adımdır. Merhaba üstbilgi değeri ile Merhaba biçimlendirilmiş `Bearer` Yetkilendirme düzeni, tek bir boşluk ve ardından hello yetkilendirme belirteci olarak başına [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). Ne yazık ki burada hello Yetkilendirme düzeni atlanmış durumlar vardır. Bu tooaccount ayrıştırılırken, biz hello üstbilgi değeri bir boşluk ve select hello son dizisini döndürülen hello dizeden bölün. Bu, hatalı biçimlendirilmiş yetkilendirme üstbilgileri için geçici bir çözüm sağlar.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Merhaba doğrulama isteği yapan
Biz hello yetkilendirme belirtecini olduktan sonra biz hello isteği toovalidate hello belirteci yapabilirsiniz. RFC 7662 bu işlem introspection çağırır ve gerektiren, `POST` bir HTML form toohello introspection kaynak. Merhaba HTML formu en az olarak hello anahtarla bir anahtar/değer çifti içermelidir `token`. Bu istek toohello yetkilendirme sunucusu ayrıca kötü amaçlı istemciler için geçerli belirteçleri trawling Git olamaz kimliği doğrulanmış tooensure olmalıdır.

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

### <a name="checking-hello-response"></a>Merhaba yanıt denetleniyor
Merhaba `response-variable-name` özniteliktir kullanılan toogive erişim hello yanıt döndürdü. Merhaba bu özelliği içinde tanımlı adı bir anahtar olarak hello kullanılabilir `context.Variables` sözlük tooaccess hello `IResponse` nesnesi.

Merhaba yanıt nesnesinden biz hello gövde alabilir ve RFC 7622 söyler, bize, hello yanıt bir JSON nesnesi olmalıdır ve adlı en az bir özellik içermelidir `active` diğer bir deyişle bir Boole değeri. Zaman `active` hello belirteci geçerli kabul doğrudur.

### <a name="reporting-failure"></a>Hata Raporlama
Kullandığımız bir `<choose>` İlkesi toodetect hello belirteci geçersiz varsa ve bu durumda, bir 401 yanıtı döndürür.

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

Göre [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) açıklayan nasıl `bearer` belirteçleri kullanılması gerekir, ayrıca döndürürüz bir `WWW-Authenticate` hello 401 yanıt üstbilgisi. Merhaba WWW-Authenticate olduğu hedeflenen tooinstruct nasıl bir istemcide tooconstruct düzgün yetkili isteği. Toohello çeşitli yaklaşımlar hello OAuth2 framework ile olası, zor olduğu tüm hello toocommunicate gerekli bilgileri. Neyse ki vardır çaba devam toohelp [istemcileri bulmak nasıl tooproperly yetkilendirmek istekleri tooa kaynak sunucusu](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Son çözüm
Tüm hello parçaları bir araya getirilmesi, biz ilke aşağıdaki hello alın:

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

Bu yalnızca nasıl birçok örnekleri biridir hello `send-request` İlkesi kullanılan toointegrate yararlı dış hizmetler isteklerin ve yanıtların hello API Management hizmet akan hello işlemine olabilir.

## <a name="response-composition"></a>Yanıt oluşturma
Merhaba `send-request` İlkesi hello önceki örnekte gördüğümüz veya tam değiştirme için hello arka uç arama kullanılan bir birincil istek tooa arka uç sistemi geliştirme için kullanılabilir. Bu teknik kullanılarak kolayca toplanır bileşik kaynakları birden çok farklı sistemlerden oluşturabiliriz.

### <a name="building-a-dashboard"></a>Bir pano oluşturma
Bazen birden fazla arka uç sistemlerinde bulunan toobe mümkün tooexpose bilgilerini örneğin, bir Pano toodrive istersiniz. Merhaba KPI'leri gelen tüm farklı arka uçları, ancak tooprovide doğrudan erişim toothem tercih ediyorsanız ve tek bir istekte tüm hello bilgisi alınamadı, iyi olacaktır. Belki de hello arka uç bilgilerin bazıları gereken bazı dilimleme ve sağlanır ve biraz önce temizleme! Bileşik kaynak yararlı tooreduce olacaktır mümkün toocache olan hello arka uç yük kendi underperforming ölçümleri değiştirirseniz, sipariş toosee hello F5 anahtar sözcüğüne alýþkanlýk kullanıcınız bildiğiniz gibi.    

### <a name="faking-hello-resource"></a>Merhaba kaynak faking
İlk adım toobuilding hello tooconfigure hello API Management yayımcı portalına yeni bir işlemde bizim Pano kaynaktır. Bu yer tutucu kullanılan işleminin tooconfigure bizim birleşim İlkesi toobuild olacaktır bizim dinamik kaynak.

![Pano işlemi](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Merhaba istekleri yapan
Bir kez hello `dashboard` işlemi oluşturulan biz özel olarak bu işlem için bir ilke yapılandırabilirsiniz. 

![Pano işlemi](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

Merhaba ilk adımı biz tooour arka uç iletebilir hello gelen istek, herhangi bir sorgu parametre tooextract aynıdır. Bu örnekte bir zaman aralığında bağlı bilgileri bizim Pano gösteren bir nedenle sahip bir `fromDate` ve `toDate` parametresi. Merhaba kullanırız `set-variable` ilke tooextract hello bilgilerini hello istek URL'si.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

Biz bu bilgileri olduktan sonra istekleri tooall hello arka uç sistemleri yapabilirsiniz. Her istek hello parametre bilgilerini içeren yeni bir URL oluşturur ve ilgili sunucusuna çağırır ve hello yanıt içeriği değişkeninde depolar.

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

Bu istekler ideal olmayan sırayla çalıştırır. Gelecek bir sürümde biz adlı yeni bir ilke size sunmuş olacağız `wait` bu istekleri tooexecute paralel olarak etkinleştirecek.

### <a name="responding"></a>Yanıt
tooconstruct hello bileşik yanıt hello kullanabileceğiniz [return yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) ilkesi. Merhaba `set-body` öğesi, bir ifade tooconstruct kullanabilir yeni `JObject` özellikleri olarak katıştırılmış tüm hello bileşen Beyanları ile.

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

Merhaba tam İlkesi şu şekilde görünür:

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

Bunu hala yeterince etkili olacaktır güncel değil, bir saat olsa bile anlamına hello veri hello yapısını anlamak için biz yapılandırabilirsiniz hello yer tutucu işlemi hello yapılandırmasında hello Pano kaynak toobe için en az bir saat önbelleğe alınan tooconvey değerli bilgiler toohello kullanıcılar.

## <a name="summary"></a>Özet
Azure API Management hizmeti, seçmeli olarak olabilir esnek ilkeler tooHTTP trafiği uygulanan sağlar ve arka uç hizmetlerinin birleşim etkinleştirir. Uyarı İşlevler, doğrulama, doğrulama yetenekleri ile API ağ geçidi tooenhance istediğiniz ya da birden fazla arka uç hizmetlerini temel alarak yeni bileşik kaynakları oluşturmak isteyip hello `send-request` ve ilgili ilkeler olanaklar dünyası açın.

## <a name="watch-a-video-overview-of-these-policies"></a>Bu ilkelerin video genel izleyin
Merhaba hakkında daha fazla bilgi için [bir şekilde İsteği Gönder](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), ve [return yanıt](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) bu makalede ele alınan ilkeleri Lütfen video aşağıdaki hello izleyin.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

