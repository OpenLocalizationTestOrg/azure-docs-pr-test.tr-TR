---
title: "aaaUse Azure AD v2.0 tooaccess, kullanıcı etkileşimi olmadan kaynakları güvenli hale getirme | Microsoft Docs"
description: "Web uygulamaları hello Azure AD uygulaması hello OAuth 2.0 kimlik doğrulama protokolü kullanarak oluşturun."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 ve hello OAuth 2.0 istemci kimlik bilgileri akış
Merhaba kullanabilirsiniz [OAuth 2.0 istemci kimlik bilgileri vermenizi](http://tools.ietf.org/html/rfc6749#section-4.4)bazen adlı *iki bacaklı OAuth*, bir uygulama hello kimliğini kullanarak tooaccess web barındırılan kaynaklar. Yaygın olarak grant bu tür bir kullanıcıyla hemen etkileşimi olmadan hello arka planda çalıştırılmalıdır server sunucusu etkileşimleri için kullanılır. Bu tür uygulamalar genellikle başvurulan tooas olan *deamon'lar* veya *hizmet hesapları*.

> [!NOTE]
> Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez. mı hello v2.0 uç kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>
>

Merhaba daha tipik olarak *üç bacaklı OAuth*, belirli bir kullanıcı adına verilen izin tooaccess bir kaynak, bir istemci uygulamasıdır. genellikle hello sırasında hello kullanıcı toohello uygulamadan Hello izin temsilci [onayı](active-directory-v2-scopes.md) işlemi. Ancak, hello istemci kimlik bilgileri akışının izinleri doğrudan toohello uygulamanın kendisinin verilir. Merhaba uygulama belirteci tooa kaynak gösterdiğinde hello kaynak hello uygulamanın kendi yetkilendirme tooperform bir eylem vardır ve bu hello kullanıcı yetkilendirme içerir zorlar.

## Protokol diyagramı
Merhaba tüm istemci kimlik bilgileri akışının benzer toohello sonraki diyagramı görünür. Biz bu makalenin sonraki bölümlerinde hello adımların her biri açıklanmaktadır.

![İstemci kimlik bilgileri akışının](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Doğrudan yetkilendirme Al
Bir uygulama genellikle doğrudan yetkilendirme tooaccess kaynak iki yoldan biriyle alır: hello kaynak, bir erişim denetim listesi (ACL) veya Azure Active Directory'de (Azure AD) uygulama izni atama. Bu iki yöntem hello Azure AD'de en yaygın olan ve bunları istemcileri ve hello istemci kimlik bilgileri akışını gerçekleştirmek kaynaklar için önerilir. Bir kaynak tooauthorize istemcilerine başka yollarla ancak seçebilirsiniz. Her kaynak sunucusu Merhaba, uygulama için en anlamlı hello yöntemi seçebilirsiniz.

### Erişim denetimi listeleri
Bir kaynak sağlayıcısı bilir ve belirli düzeyde bir erişim verir uygulama kimlikleri listesini dayalı bir yetkilendirme onay zorlayabilir. Hello kaynak hello v2.0 uç noktasından belirteç aldığında, bu hello belirteç kodunu çözer ve hello hello istemcinin uygulama kimliği ayıklamak `appid` ve `iss` talep. Ardından Merhaba uygulaması sakladığı bir ACL karşı karşılaştırır. ACL'leri ayrıntı düzeyi hello ve yöntemi kaynaklar arasında önemli ölçüde farklılık gösterebilir.

Bir ortak kullanım Web API'sini veya bir web uygulaması için bir ACL toorun testleri toouse durumdur. Merhaba Web API yalnızca bir alt kümesini tam izinleri tooa belirli istemci için izin verebilir. Merhaba API, toorun uçtan uca testleri belirteçleri hello v2.0 uç noktasından alır ve bunları toohello API gönderen bir test istemcisi oluşturun. Merhaba API sonra denetimleri hello ACL hello için tam erişim toohello API'nin tüm işlevselliği için istemcinin uygulama kimliği sınayın. Bu tür bir ACL kullanıyorsanız toovalidate yalnızca arayanın hello unutmayın `appid` değeri. Ayrıca bu hello doğrulamak `iss` hello belirteç değeri güvenilir.

Bu tür bir kimlik doğrulama, arka plan programları ve kişisel Microsoft hesabına sahip tüketici kullanıcılara ait tooaccess verilere ihtiyaç hizmet hesapları için yaygındır. Kuruluşlar tarafından ait verileri için hello gerekli yetkilendirme uygulama izinleri aracılığıyla elde etmenizi öneririz.

### Uygulama izinleri
ACL'ler kullanmak yerine, API tooexpose uygulama izinleri kullanabilirsiniz. Bir uygulama izni tooan uygulama bir kuruluşun Yöneticisi tarafından verilir ve kullanılan yalnızca tooaccess verileri belirli bir kuruluş ve çalışanlarının tarafından ait olabilir. Örneğin, Microsoft Graph birkaç uygulama izinleri toodo hello şunları sunar:

* Tüm posta kutularındaki postaları okuma
* Tüm posta kutularındaki postaları okuma ve yazma
* Herhangi bir kullanıcı adına posta gönderme
* Dizin verilerini okuma

Uygulama izinleri hakkında daha fazla bilgi için çok Git[Microsoft Graph](https://graph.microsoft.io).

uygulamanızda toouse uygulama izinleri hello sonraki bölümlerde aşağıdakiler ele adımları hello.

#### Merhaba uygulama kayıt Portalı'nda Hello izinleri iste
1. Merhaba tooyour uygulamada Git [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya [bir uygulama oluşturmak](active-directory-v2-app-registration.md), henüz yapmadıysanız. Toouse gerekir en az bir uygulama, uygulamanızı oluştururken gizli anahtarı.
2. Merhaba bulun **doğrudan uygulama izinleri** bölümünde ve ardından uygulamanızı gerektirir hello izinleri ekleyin.
3. **Kaydet** hello uygulama kaydı.

#### Önerilir: Tooyour uygulamasında oturum hello kullanıcı
Genellikle, uygulama izinleri kullanan bir uygulama oluşturduğunuzda, hello uygulama sayfa veya hangi hello üzerinde yönetici hello uygulamanın izinleri onaylar görünüm gerektirir. Bu sayfayı hello uygulamanın oturum açma akışını, hello uygulamanın ayarlarının bir parçası parçası olabilir veya ayrılmış bir "akış Bağlan" olabilir. Çoğu durumda, hello uygulama tooshow için bu "yalnızca bir kullanıcı bir iş veya Okul Microsoft hesabı oturum imzaladığı sonra bağlantı görünümü" mantıklıdır.

Merhaba kullanıcı tooyour uygulamasında oturum açarsanız, hello kuruluş tanımlayabilirsiniz toowhich hello kullanıcının ait olduğu önce hello kullanıcı tooapprove hello uygulama izinleri isteyin. Kesinlikle gerekli olmasa da, kullanıcılarınızın daha sezgisel bir deneyim oluşturmanıza yardımcı olabilir. uygulamasında, izleme toosign hello kullanıcı bizim [v2.0 protokol öğreticileri](active-directory-v2-protocols.md).

#### Bir dizin yöneticisinden gelen isteği hello izinleri
Merhaba kuruluşunuzun yöneticisiyle hazır toorequest izinlerinin olduğunuzda hello kullanıcı toohello v2.0 yönlendirebilirsiniz *yönetici onayı uç noktası*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parametre | Koşul | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |toorequest izni istediğiniz hello directory kiracısı. Bu GUID veya kolay ad biçiminde olabilir. Hangi Kiracı hello kullanıcının ait olduğu tüm Kiracı oturum kullanım oturumunu toolet istediğiniz tooand tanımadığınız varsa `common`. |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour uygulama atanmış. |
| redirect_uri |Gerekli |Merhaba, uygulama toohandle için gönderilen hello yanıt toobe istediğiniz URI yönlendirin. URL kodlanmış olmalıdır ancak bu, tam olarak hello yeniden yönlendirme hello Portalı'nda kayıtlı URI'ler eşleşmelidir ve ek yol kesimine sahip olabilir. |
| durum |Önerilen |Merhaba, aynı zamanda isteğinde bir değer hello belirteci yanıt olarak döndürülür. İstediğiniz herhangi bir içerik dizesi olabilir. hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |

Bu noktada, Azure AD yalnızca bir kiracı Yöneticisi toocomplete hello istekte oturum açarak zorlar. Hello Yöneticisi tüm hello uygulama kayıt Portalı'nda, uygulamanız için istenen doğrudan uygulama izinleri hello tooapprove istenir.

##### Başarılı yanıt
Hello Yöneticisi uygulamanızı hello izinlerini onaylarsa, hello başarılı yanıtı şuna benzer:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parametre | Açıklama |
| --- | --- | --- |
| Kiracı |Uygulama hello izinlerinizi verilen hello dizin Kiracı bunu, GUID biçiminde istedi. |
| durum |Merhaba, aynı zamanda isteğinde bir değer hello belirteci yanıt olarak döndürülür. İstediğiniz herhangi bir içerik dizesi olabilir. hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |
| admin_consent |Çok ayarlamak**doğru**. |

##### Hata yanıtı
Hello Yöneticisi uygulamanızı hello izinlerini onaylamaz, bu yanıt görülüyor hello başarısız oldu:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parametre | Açıklama |
| --- | --- | --- |
| error |Tooclassify türleri kullanabileceğiniz bir hata kodu dizesi hataları ve hangi tooreact tooerrors kullanabilirsiniz. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi hello kök bir hatanın nedenini belirleyin. |

Merhaba uygulama sağlama uç noktasından başarılı bir yanıt aldık sonra uygulamanızı istendiğinde hello doğrudan uygulama izinleri kazanmıştır. Şimdi istediğiniz hello kaynak için bir belirteç talep edebilirsiniz.

## Belirteç alın
Uygulamanız için hello gerekli yetkilendirme edindiğiniz sonra erişim belirteçleri API'ler alınırken ile devam edin. tooget hello istemci kimlik bilgileri sağlama kullanarak bir belirteç Gönder bir POST isteği toohello `/token` v2.0 uç noktası:

### İlk durumda: bir paylaşılan gizlilik ile erişim belirteci isteği

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Parametre | Koşul | Açıklama |
| --- | --- | --- |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour uygulama atanmış. |
| Kapsam |Gerekli |Merhaba geçirildi Merhaba `scope` bu isteği parametresinde istediğiniz ile Merhaba yapıştırılmış hello kaynağının hello kaynak tanımlayıcısı (uygulama kimliği URI) olmalıdır `.default` soneki. Merhaba Microsoft Graph örneğin hello değerdir `https://graph.microsoft.com/.default`. Bu değer hello v2.0 uç noktası, uygulamanız için yapılandırdığınız tüm hello doğrudan uygulama izinleriyle onu hello istediğiniz hello kaynakla ilişkili olanlar için bir belirteç toouse yayımlamalısınız olduğunu bildirir. |
| client_secret |Gerekli |Merhaba hello uygulama kayıt Portalı'nda, uygulamanız için oluşturulan uygulama gizli. |
| grant_type |Gerekli |Olmalıdır `client_credentials`. |

### İkinci durumda: bir sertifika ile erişim belirteci isteği

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Parametre | Koşul | Açıklama |
| --- | --- | --- |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour uygulama atanmış. |
| Kapsam |Gerekli |Merhaba geçirildi Merhaba `scope` bu isteği parametresinde istediğiniz ile Merhaba yapıştırılmış hello kaynağının hello kaynak tanımlayıcısı (uygulama kimliği URI) olmalıdır `.default` soneki. Merhaba Microsoft Graph örneğin hello değerdir `https://graph.microsoft.com/.default`. Bu değer hello v2.0 uç noktası, uygulamanız için yapılandırdığınız tüm hello doğrudan uygulama izinleriyle onu hello istediğiniz hello kaynakla ilişkili olanlar için bir belirteç toouse yayımlamalısınız olduğunu bildirir. |
| client_assertion_type |Gerekli |Merhaba değeri olmalıdır`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Gerekli | Uygulamanız için kimlik bilgileri olarak toocreate gerekir ve hello işaretiyle sertifika onayı ifade (bir JSON Web belirteci) kayıtlı. Hakkında bilgi edinin [sertifika kimlik bilgileri](active-directory-certificate-credentials.md) toolearn nasıl tooregister hello onaylama, sertifika ve hello biçimi.|
| grant_type |Gerekli |Olmalıdır `client_credentials`. |

Neredeyse olarak hello parametreleridir bildirimi hello hello isteği hello durumunda olduğu gibi aynı tarafından paylaşılan gizliliği hello client_secret parametresi tarafından iki parametre değiştirilir dışında: client_assertion_type ve client_assertion.

### Başarılı yanıt
Başarılı yanıt şöyle görünür:

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Parametre | Açıklama |
| --- | --- |
| access_token |Merhaba istenen erişim belirteci. Merhaba uygulama tooa Web API gibi kaynak güvenli Bu belirteci tooauthenticate toohello kullanabilirsiniz. |
| token_type |Merhaba belirteç türü değeri gösterir. yalnızca Azure AD destekler türü hello `bearer`. |
| expires_in |Ne kadar süreyle hello erişim belirteci (saniye olarak) geçerli değil. |

### Hata yanıtı
Bir hata yanıtı şuna benzer:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parametre | Açıklama |
| --- | --- |
| error |Tooclassify türlerini oluşan hataları ve tooreact tooerrors kullanabileceğiniz bir hata kodu dizesi. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| error_codes |Tanılama ile yardımcı olabilecek STS özgü hata kodları listesi. |
| timestamp |Merhaba hata gerçekleştiği hello süre. |
| trace_id |Tanılama ile yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |
| correlation_id |Tanılama ile bileşenlerinde yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |

## Bir belirteci kullanın
Bir belirteç edindiğiniz, hello belirteci toomake istekleri toohello kaynağı kullanın. Merhaba belirtecinin süresi dolduğunda, hello isteği toohello yineleyin `/token` uç nokta tooacquire yeni erişim belirteci.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Kod örneği
toosee uygulayan hello yönetici onayı uç noktası, kullanarak istemci kimlik bilgileri sağlama hello bir örnek uygulamanın bkz bizim [v2.0 arka plan kod örneği](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
