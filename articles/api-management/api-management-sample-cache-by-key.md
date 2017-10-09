---
title: "Azure API Management'te aaaCustom önbelleğe alma"
description: "Azure API Management'te anahtarı tarafından nasıl toocache öğelerini öğrenin"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a>Azure API Management'te özel önbelleğe alma
Azure API Management hizmeti için yerleşik destek sahip [HTTP yanıt önbelleğe alma](api-management-howto-cache.md) hello kaynak URL hello anahtar olarak kullanma. Merhaba anahtar hello kullanarak istek üstbilgileri tarafından değiştirilebilir `vary-by` özellikleri. Tüm HTTP yanıtlarını (diğer adıyla Beyanları) önbelleğe alma işlemi için kullanışlıdır ancak bazen yararlı toojust önbellek temsili bir bölümü olabilir. Merhaba yeni [önbellek arama değeri](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) ve [önbellek deposu değeri](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) ilkeler ilke tanımları içindeki verileri toostore ve alma rasgele parçalarını hello olanağı sağlar. Bu yeteneği de daha önce eklenen değer toohello ekler [gönderme isteği](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) İlkesi çünkü dış hizmetler yanıtlarının şimdi önbelleğe alabilir.

## <a name="architecture"></a>Mimari
API Management hizmeti kullanan bir kiracı başına paylaşılan veri önbelleği toomultiple birimler ölçeklendirmenize göre erişim toohello hala alırsınız böylece aynı verileri önbelleğe. Ancak, bölgeli dağıtımı ile çalışırken, her hello bölgelerinin bağımsız önbellekleri vardır. Son toothis, onu önemlidir toonot hello önbellek hello yalnızca kaynak bilgileri parçasının olduğu bir veri deposu olarak ele alın. Vermedi ve daha sonra hello bölgeli dağıtım tootake avantajlarından karar, seyahat kullanıcılar müşterilerle erişim önbelleğe toothat veri kaybedebilir.

## <a name="fragment-caching"></a>Parça önbelleğe alma
Burada verilen yanıtları pahalı toodetermine ve makul bir süre için henüz yeni kalan verileri kısmı içeren bazı durumlar vardır. Örnek olarak, Uçuş Rezervasyonları, uçuş durumu ile ilgili bilgi sağlayan bir uçak tarafından oluşturulmuş bir hizmeti kullanmayı düşünün. Merhaba kullanıcı hello airlines noktaları program üyesi ise, bunlar tootheir geçerli durumu ve toplanan mesafe ilgili bilgileri de gerekir. Bu kullanıcı ile ilgili bilgiler farklı depolanabilir, ancak uçuş durumu ve ayırmaları hakkında yanıtlarındaki döndürdüğü arzu tooinclude olabilir. Bu yapılabilir parça önbelleğe alma adlı bir işlem kullanılarak. Merhaba birincil gösterimi hello kullanıcıyla ilişkili bilgileri eklenen toobe olduğu belirteci tooindicate çeşit kullanılarak hello kaynak sunucudan döndürülebilir. 

Arka uç API yanıtından JSON aşağıdaki hello göz önünde bulundurun.

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

Ve ikincil kaynakta `/userprofile/{userid}` olduğunu gibi görünüyor,

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

Sipariş toodetermine hello uygun kullanıcı bilgileri tooinclude içinde hello son kullanıcıdan tooidentify gerekir. Bu mekanizma bağımlı uygulamasıdır. Örnek olarak, hello kullanıyorum `Subject` , talep bir `JWT` belirteci. 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

Bu depolarız `enduserid` daha sonra kullanmak için bir bağlam değişken değeri. önceki bir istek varsa zaten hello kullanıcı bilgileri alınır ve hello önbellekte depolanan hello sonraki toodetermine adımdır. Merhaba bu için kullandığımız `cache-lookup-value` ilkesi.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

Toohello anahtar değeri ve ardından Hayır karşılık gelen hello önbelleğinde girişi yoksa `userprofile` bağlamının oluşturulur. Biz hello kullanarak hello araması hello başarısını denetleyin `choose` kontrol akışı ilkesi.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Merhaba, `userprofile` bağlamının yok ve devam eden toohave toomake bir HTTP isteği tooretrieve gerçekleştiriyoruz.

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

Merhaba kullanırız `enduserid` tooconstruct hello URL toohello kullanıcı profili kaynağı. Biz hello yanıt olduktan sonra biz hello gövde metni hello yanıt dışında çekme ve bir bağlam değişkende saklayın.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid bize hello aynı kullanıcı başka bir istekte bulunduğunda toomake bu HTTP isteği yeniden sahip, biz hello kullanıcı profili hello önbellekte saklayabilirsiniz.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Biz başlangıçta tooretrieve çalıştı hello tam aynı anahtarı kullanarak hello Önbelleği'nde hello değeri depolarız ile. Merhaba toostore hello değeri seçeneğini belirledik süresi ne sıklıkta hello bilgi değişikliklerini ve nasıl dayanıklı kullanıcılar tarih bilgisi tooout olduğuna bağlı olmalıdır. 

Bu önemli toorealize hello önbellekten hala olduğundan bir işlem dışı, ağ isteği ve potansiyel olarak milisaniye toohello isteği onlarca eklemeye devam edebilirsiniz. belirleme hello kullanıcı profili bilgilerini daha önemli ölçüde uzun son tooneeding toodo veritabanı sorguları veya birden fazla arka uç toplama bilgilerinden yönlendirdiğinde hello avantajları gelir.

Merhaba son hello işleminde bizim kullanıcı profili bilgilerini içeren bir yanıt döndürdü tooupdate hello adımdır.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

Böylece hello Değiştir bile gerçekleşmezse, hello yanıt hala geçerli JSON zamanki tooinclude hello tırnak işaretleri hello belirtecinin bir parçası seçtiğim. Öncelikle daha kolay hata ayıklama toomake oluştu.

Tüm adımları birleştirmek sonra hello sonuç hello bir aşağıdaki gibi görünen bir ilkedir.

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

Önbelleğe alma bu yaklaşım, tek bir sayfa olarak işlenebilecek böylece burada HTML hello sunucu tarafında oluşur web siteleri, öncelikle kullanılır. Ancak, bu da yararlı olabilir burada istemcileri bulunulamaz istemci API'ları yan HTTP önbelleğe alma veya tercih edilir değil tooput bu sorumluluğu hello istemcide.

Parça önbelleğe alma bu aynı tür, sunucu önbelleği Redis hello arka uç web sunucularında kullanılarak yapılabilir, önbelleğe alınmış hello parçaları hello'den farklı arka uçları'ten gelen ancak hello API Management hizmeti tooperform kullanarak bu iş kullanışlıdır Birincil yanıtlar.

## <a name="transparent-versioning"></a>Saydam sürüm oluşturma
Desteklenen herhangi bir anda bir API toobe birden çok farklı uygulama sürümlerini yaygın bir uygulamadır. Bu belki de geliştirme, test, üretim, vb., gibi toosupport farklı ortamlar veya hello API toogive zaman API tüketicileri toomigrate toonewer sürümleri için eski sürümleri toosupport olabilir. 

İstemci geliştiricilerin toochange hello URL'lerden gerektiren bu bunun yerine, bir yaklaşım toohandling `/v1/customers` çok`/v2/customers` toostore hello tüketicinin profil verileri de hello API'ın hangi sürümü bunlar şu anda toouse istiyor ve çağırın hello uygun değil arka uç URL'si. İsteğe bağlı olarak belirli bir istemci için sipariş toodetermine hello doğru arka uç URL'si toocall içinde gerekli tooquery olan bazı yapılandırma verileri. Bu yapılandırma verileri önbelleğe alarak Biz bu Arama yapmanın hello performans cezası en aza indirebilirsiniz.

Merhaba ilk adımı toodetermine hello tanımlayıcı tooconfigure hello istediğiniz sürümü kullanılır. Bu örnekte, t tooassociate hello sürüm toohello ürün abonelik anahtarı seçtiniz. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

Biz hello istenen istemci sürümü aldıktan, biz sonra bir önbellek arama toosee yapın.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

Biz bunu hello önbelleğinde bulamadı olmadığını biz toosee denetleyin.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Git ve bunu alma sonra biz almadıysanız.

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

Merhaba yanıt gövdesi metni hello yanıttan ayıklayın.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Gelecekte kullanım için hello önbelleğindeki geri depolar.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

Ve son olarak hello arka uç URL'si tooselect hello hello istemci tarafından istenen hello hizmetinin sürümünü güncelleştirin.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Merhaba tamamen ilke aşağıdaki gibidir.

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

Hangi arka uç sürümü tooupdate ve yeniden dağıtın istemcileri gerek kalmadan istemciler tarafından erişiliyor API tüketicileri tootransparently denetimini etkinleştirme birçok API sürüm oluşturma sorunları ele zarif bir çözümdür.

## <a name="tenant-isolation"></a>Kiracı yalıtımı
Daha büyük, çok kiracılı dağıtımlarda bazı şirketler, arka uç donanım ayrı dağıtımlarına kiracılar ayrı grupları oluşturun. Bu bir donanım sorunu hello arka uç tarafından etkilenen müşteriler hello sayısını en aza indirir. Ayrıca, yeni yazılım sürümleri toobe aşamada alındı sağlar. İdeal olarak bu arka uç mimarisi saydam tooAPI tüketicileri olmalıdır. Merhaba üzerinde dayandığından bu benzer bir şekilde tootransparent sürüm oluşturma sağlanabilir API anahtarı başına yapılandırma durumu kullanarak hello arka uç URL'si düzenleme aynı tekniği.  

Merhaba API her abonelik anahtarı için tercih edilen bir sürümünü döndürme yerine bir kiracı atanan toohello donanım grubu ilişkili tanımlayıcı döndürecektir. Bu tanımlayıcı, kullanılan tooconstruct hello uygun arka uç URL'si olabilir.

## <a name="summary"></a>Özet
Hello özgürlük toouse hello Azure API management önbellek her türlü veri depolamak için bir gelen talep işlenen hello biçimini etkileyebilir etkili erişim tooconfiguration veri sağlar. Ayrıca, arka ucundan API döndürülen yanıt genişletebilirsiniz kullanılan toostore veri parçaları de olabilir.

## <a name="next-steps"></a>Sonraki adımlar
Bu ilkeler için etkinleştirdiğiniz, veya senaryoları varsa tooachieve istediğiniz ancak değil düşündüğünüz diğer senaryolar şu anda olası varsa lütfen bize Geri bildiriminizi hello Disqus iş parçacığı için bu konunun verin.

