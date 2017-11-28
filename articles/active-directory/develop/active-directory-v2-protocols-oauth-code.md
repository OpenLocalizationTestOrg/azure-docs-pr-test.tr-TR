---
title: "aaaAzure AD v2.0 OAuth yetkilendirme kod akış | Microsoft Docs"
description: "Azure AD uygulaması hello OAuth 2.0 kimlik doğrulama protokolü kullanarak web uygulamaları oluşturma."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# v2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı
Merhaba OAuth 2.0 yetkilendirme kodu verme, bir aygıt toogain tooprotected erişimine, web API'leri gibi yüklenen uygulamalarda kullanılabilir.  OAuth 2.0 Hello uygulama modeli v2.0 's uygulaması kullanarak, oturum açma ve API erişim tooyour mobil ve Masaüstü uygulamaları ekleyebilirsiniz.  Bu kılavuz dilden bağımsızdır ve açıklar nasıl toosend ve bizim açık kaynak kitaplıkları kullanmadan HTTP iletileri alabilirsiniz.

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

Merhaba OAuth 2.0 yetkilendirme kodu akışını içinde açıklanan [4.1 hello OAuth 2.0 belirtimi bölüm](http://tools.ietf.org/html/rfc6749).  Kullanılan tooperform kimlik doğrulama ve yetkilendirme dahil olmak üzere uygulama türleri hello çoğunluğu olan [web uygulamaları](active-directory-v2-flows.md#web-apps) ve [uygulamaları'yerel olarak yüklenen](active-directory-v2-flows.md#mobile-and-native-apps).  Toosecurely elde hello v2.0 uç noktası kullanılarak güvenlik altına kullanılan tooaccess kaynakları olabilen access_tokens uygulamaları etkinleştirir.  

## Protokol diyagramı
Yerel/mobil uygulama için hello tüm kimlik doğrulama akışı, yüksek düzeyde, şöyle bir bit görünür:

![OAuth kimlik doğrulama kodu akışı](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## İstek bir kimlik doğrulama kodu
Merhaba yetkilendirme kodu akışı başlar hello kullanıcı toohello yönlendirerek hello istemcisiyle `/authorize` uç noktası.  Bu istekte hello istemci hello kullanıcıdan tooacquire gereken hello izinleri gösterir:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Bu istek tooexecute Hello bağlantıya tıklayın! Oturum açtıktan sonra tarayıcınızı çok yeniden yönlendirilmesi gereken`https://localhost/myapp/` ile bir `code` hello adres çubuğundaki.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://Login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: `common`, `organizations`, `consumers`ve Kiracı tanımlayıcıları.  Daha fazla ayrıntı için [protokol Temelleri](active-directory-v2-protocols.md#endpoints). |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello kayıt portalı ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) uygulamanızı atanmış. |
| response_type |Gerekli |İçermelidir `code` hello yetkilendirme kodu akışı. |
| redirect_uri |Önerilen |Burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan, uygulamanızın Hello redirect_uri.  Bu tam olarak bir url kodlanmış olmalıdır dışında hello Portalı'nda kayıtlı hello redirect_uris eşleşmelidir.  Yerel & mobil uygulamaları için hello varsayılan değeri kullanması gereken `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| Kapsam |Gerekli |Boşlukla ayrılmış bir listesini [kapsamları](active-directory-v2-scopes.md) hello kullanıcı tooconsent istiyor. |
| response_mode |Önerilen |Kullanılan toosend hello elde edilen belirteci geri tooyour uygulama olmalıdır hello yöntemini belirtir.  Olabilir `query` veya `form_post`. |
| durum |Önerilen |Hello belirteci yanıt olarak da döndürülür hello istekte bulunan bir değer.  İstediğiniz herhangi bir içerik dizesi olabilir.  Rastgele oluşturulan benzersiz bir değer tipik olarak kullanılan [siteler arası istek sahteciliğini saldırılarını önleme](http://tools.ietf.org/html/rfc6749#section-10.12).  hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |
| istemi |İsteğe bağlı |Gerekli bir kullanıcı etkileşimi Hello türünü belirtir.  Yalnızca şu anda geçerli değerler 'oturum açma', 'none' hello ve 'onay'.  `prompt=login`zorla kullanıcı tooenter üzerinde çoklu oturum negating bu isteğin kimlik bilgilerini hello.  `prompt=none`Ters hello - hello kullanıcının hiçbir etkileşimli istemi doğabilecek sunulmayan sağlayacak olur.  Merhaba isteği sessizce çoklu oturum açma aracılığıyla tamamlanamazsa, hello v2.0 uç noktası bir hata döndürür.  `prompt=consent`Tetikleyici hello OAuth hello kullanıcı toogrant izinleri toohello uygulama soran iletişim hello kullanıcı işaretleri, sonra onay. |
| login_hint |İsteğe bağlı |Olması kullanılan toopre dolgu hello kullanıcı adı/e-posta adresi alanı hello uygulamasında oturum açabilir sayfa hello kullanıcı için kullanıcı adı önceden biliyorsanız.  Bir önceki oturum bileşeninden hello kullanıcı adı zaten ayıklanan yeniden kimlik doğrulaması sırasında bu parametre genellikle uygulamaları kullanacak hello kullanarak `preferred_username` talep. |
| domain_hint |İsteğe bağlı |Aşağıdakilerden biri olabilir `consumers` veya `organizations`.  Dahil edilmişse, hello e-posta tabanlı bulma işlemi atlar kullanıcı hello v2.0 oturum açma sayfası, üzerinde önde gelen tooa biraz daha verimli bir kullanıcı deneyimi geçtiği.  Genellikle uygulamaları kullanacağınız Bu parametre yeniden kimlik doğrulaması sırasında hello çıkartarak `tid` gelen bir önceki oturum açma.  Merhaba, `tid` değer talep `9188040d-6c67-4c5b-b112-36a304b66dad`, kullanmanız gereken `domain_hint=consumers`.  Aksi takdirde kullanın `domain_hint=organizations`. |

Bu noktada, hello kullanıcı olacaktır tooenter kendi kimlik bilgilerini ve tam hello kimlik doğrulaması istedi.  Hello v2.0 uç noktası da o hello kullanıcı hello belirtilen toohello izinleri rıza sağlayacak `scope` sorgu parametresi.  Merhaba kullanıcı tooany bu izin verdiği değil, bu hello kullanıcı tooconsent toohello gerekli izinleri sorar.  Ayrıntılarını [izinleri, onay ve çok kiracılı uygulamalara sağlanan burada](active-directory-v2-scopes.md).

Merhaba kullanıcı kimliğini doğrular ve izin veren sonra hello v2.0 uç hello belirtilen bir yanıt tooyour uygulamaya döndürülecek `redirect_uri`, hello belirtilen hello yöntemi kullanarak `response_mode` parametresi.

#### Başarılı yanıt
Başarılı yanıt kullanarak `response_mode=query` gibi görünüyor:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Parametre | Açıklama |
| --- | --- |
| Kod |İstenen uygulama hello hello authorization_code. Merhaba uygulama hello yetkilendirme kodu toorequest bir erişim belirteci hello hedef kaynak için kullanabilirsiniz.  Authorization_codes çok kısa süreli, genellikle bu, yaklaşık 10 dakika sonra süresi dolacak. |
| durum |Bir durum parametresi hello istekte yer alıyorsa hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama hello durum değerleri hello istek ve yanıtta özdeş olduğunu doğrulamanız gerekir. |

#### Hata yanıtı
Hata yanıtları toohello da gönderilebilir `redirect_uri` hello uygulama bunları uygun şekilde işleyebilmesi için:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

#### Yetkilendirme uç noktası hataları için hata kodları
Merhaba aşağıdaki tabloda açıklanmaktadır hello hello döndürülebilecek çeşitli hata kodları `error` hello hata yanıtı parametresi.

| Hata kodu | Açıklama | İstemci eylemi |
| --- | --- | --- |
| invalid_request |Eksik gerekli parametre gibi protokol hatası. |Düzeltin ve hello isteği yeniden gönderin. Bir geliştirme budur hata genellikle yakalanan ilk test sırasında. |
| unauthorized_client |Merhaba istemci uygulaması olmadığından toorequest bir yetki kodu izin verilir. |Bu durum genellikle, Merhaba istemci uygulaması Azure AD'de kayıtlı değil veya toohello kullanıcının Azure AD kiracısı eklenmez genellikle ortaya çıkar. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |
| ACCESS_DENIED |Kaynak sahibi izin reddedildi |Merhaba istemci uygulaması hello kullanıcı izin sürece devam edemiyor hello kullanıcı bildirebilir. |
| unsupported_response_type |Merhaba yetkilendirme sunucusu hello istekte hello yanıt türünü desteklemiyor. |Düzeltin ve hello isteği yeniden gönderin. Bir geliştirme budur hata genellikle yakalanan ilk test sırasında. |
| server_error |Merhaba sunucu beklenmeyen bir hatayla karşılaştı. |Merhaba isteği yeniden deneyin. Bu hatalar geçici koşulları neden olabilir. Merhaba istemci uygulaması toohello kullanıcı açıklayan, yanıtını geçici bir hata ertelendi. |
| temporarily_unavailable |Merhaba geçici olarak meşgul toohandle hello isteği sunucusudur. |Merhaba isteği yeniden deneyin. Merhaba istemci uygulaması toohello kullanıcı açıklayan, yanıtını geçici bir durum ertelendi. |
| invalid_resource |Merhaba hedef kaynak mevcut değil, Azure AD, bulunamıyor veya düzgün yapılandırılmamış olduğundan geçerli değil. |Bu, varsa, hello kaynak hello Kiracı yapılandırılmadı gösterir. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |

## İstek bir erişim belirteci
Bir authorization_code edindiğiniz ve hello kullanıcı tarafından izin verilen göre hello kullanmak `code` için bir `access_token` toohello göndererek kaynağı, istenen bir `POST` toohello isteği `/token` uç noktası:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Postman içinde bu isteği yürütmeden deneyin! (Tooreplace hello unutmayın `code`) [ ![Postman Çalıştır](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: `common`, `organizations`, `consumers`ve Kiracı tanımlayıcıları.  Daha fazla ayrıntı için [protokol Temelleri](active-directory-v2-protocols.md#endpoints). |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello kayıt portalı ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) uygulamanızı atanmış. |
| grant_type |Gerekli |Olmalıdır `authorization_code` hello yetkilendirme kodu akışı. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi.  Merhaba kapsamları hello ilk leg içinde eşdeğer tooor hello kapsamları bir kısmı bu leg istenen gerekir istedi.  Bu istekte belirtilen hello kapsamları birden çok kaynak sunucuları yayılıyorsa hello v2.0 uç hello ilk kapsamında belirtilen hello kaynak için bir belirteç döndürür.  Kapsamları hakkında daha ayrıntılı açıklaması için çok başvuran[izinleri, onay ve kapsamları](active-directory-v2-scopes.md). |
| Kod |Gerekli |Merhaba akışının hello ilk leg aldığınız hello authorization_code. |
| redirect_uri |Gerekli |kullanılan tooacquire hello authorization_code olduğu aynı redirect_uri değeri hello. |
| client_secret |Web uygulamaları için gerekli |Merhaba uygulama kayıt Portalı'nda uygulamanız için oluşturduğunuz hello uygulama gizli anahtarı.  Client_secrets güvenilir bir şekilde cihazlarda depolanamaz çünkü yerel bir uygulamada kullanılmamalıdır.  Web uygulamaları ve web hello özelliği toostore hello client_secret güvenli bir şekilde hello sunucu tarafında sahip API'leri için gereklidir. |

#### Başarılı yanıt
Başarılı bir token yanıt gibi görünür:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parametre | Açıklama |
| --- | --- |
| access_token |Merhaba istenen erişim belirteci. Merhaba uygulaması web API'si gibi kaynak güvenli Bu belirteci tooauthenticate toohello kullanabilir. |
| token_type |Merhaba belirteç türü değeri gösterir. Hello Azure AD destekleyen türü olan taşıyıcı |
| expires_in |Ne kadar süreyle hello erişim belirteci (saniye olarak) geçerli değil. |
| Kapsam |access_token hello hello kapsamlar için geçerlidir. |
| refresh_token |Bir OAuth 2.0 yenileme belirteci. Merhaba uygulama bu belirteci kullanabilirsiniz hello geçerli erişim belirtecinin süresi dolduktan sonra ek erişim belirteçleri almak.  Refresh_tokens uzun süreli ve uzun süre için kullanılan tooretain erişim tooresources olabilir.  Daha fazla ayrıntı için toohello başvuran [v2.0 belirteç başvurusu](active-directory-v2-tokens.md). |
| id_token |Bir imzasız JSON Web Token (JWT). Merhaba uygulama can base64Url açtığınız hello kullanıcının bu belirteci toorequest bilgilerini hello kesimleri kodunu çözer. Hello uygulama hello değerleri önbelleğe ve bunları görüntüler, ancak, bunlar üzerinde herhangi bir yetkilendirme veya güvenlik sınırları için güvenmemelisiniz.  Merhaba id_tokens hakkında daha fazla bilgi için bkz: [v2.0 uç noktası belirteç başvurusu](active-directory-v2-tokens.md). |

#### Hata yanıtı
Hata yanıtları gibi görünür:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| error_codes |Tanılamada yardımcı olabilecek STS belirli hata kodlarının listesi. |
| timestamp |Merhaba hata gerçekleştiği hello süre. |
| trace_id |Tanılamada yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |
| correlation_id |Tanılama'bileşenlerinde yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |

#### Belirteç uç noktası hataları için hata kodları
| Hata kodu | Açıklama | İstemci eylemi |
| --- | --- | --- |
| invalid_request |Eksik gerekli parametre gibi protokol hatası. |Düzeltin ve hello isteği yeniden gönderin |
| invalid_grant |Merhaba yetkilendirme kodu geçersiz veya süresi doldu. |Yeni bir istek toohello deneyin `/authorize` uç noktası |
| unauthorized_client |Merhaba kimliği doğrulanmış istemci yetkilendirilmez toouse Bu yetki türü. |Bu durum genellikle, Merhaba istemci uygulaması Azure AD'de kayıtlı değil veya toohello kullanıcının Azure AD kiracısı eklenmez genellikle ortaya çıkar. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |
| invalid_client |İstemci kimlik doğrulaması başarısız oldu. |Merhaba istemci kimlik bilgileri geçerli değil. toofix, hello Uygulama Yöneticisi hello kimlik bilgilerini güncelleştirir. |
| unsupported_grant_type |Merhaba yetkilendirme sunucusu hello yetkilendirme verme türünü desteklemiyor. |Değişiklik hello hello istek türü verin. Bu tür bir hata yalnızca geliştirme sırasında gerçekleşmesi gerektiğini ve ilk test sırasında algılandı. |
| invalid_resource |Merhaba hedef kaynak mevcut değil, Azure AD, bulunamıyor veya düzgün yapılandırılmamış olduğundan geçerli değil. |Bu, varsa, hello kaynak hello Kiracı yapılandırılmadı gösterir. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |
| interaction_required |Merhaba isteği kullanıcı etkileşimi gerektirir. Örneğin, bir ek kimlik doğrulama adım gereklidir. |Merhaba Hello istekle yeniden deneme aynı kaynak. |
| temporarily_unavailable |Merhaba geçici olarak meşgul toohandle hello isteği sunucusudur. |Merhaba isteği yeniden deneyin. Merhaba istemci uygulaması toohello kullanıcı açıklayan, yanıtını geçici bir durum ertelendi. |

## Merhaba erişim belirteci kullanın
Başarıyla edindiğiniz göre bir `access_token`, hello dahil ederek istekleri tooWeb API'leri hello belirteci kullanabilirsiniz `Authorization` üstbilgisi:

> [!TIP]
> Bu istek içinde Postman yürütme! (Hello yerine `Authorization` üstbilgi ilk) [ ![Postman Çalıştır](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Merhaba erişim belirteci Yenile
Access_tokens kısa süreli ve kaynaklara erişme toocontinue parolalarının süresi dolduktan sonra bunları yenilemeniz gerekir.  Başka bir göndererek yapabilirsiniz `POST` toohello isteği `/token` uç noktası, hello sağlayarak bu kez `refresh_token` hello yerine `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Postman içinde bu isteği yürütmeden deneyin! (Tooreplace hello unutmayın `refresh_token`) [ ![Postman Çalıştır](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: `common`, `organizations`, `consumers`ve Kiracı tanımlayıcıları.  Daha fazla ayrıntı için [protokol Temelleri](active-directory-v2-protocols.md#endpoints). |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello kayıt portalı ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) uygulamanızı atanmış. |
| grant_type |Gerekli |Olmalıdır `refresh_token` bu leg hello yetkilendirme kodu akışı için. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi.  Merhaba kapsamları hello özgün authorization_code isteği leg içinde eşdeğer tooor hello kapsamları bir kısmı bu leg istenen gerekir istedi.  Bu istekte belirtilen hello kapsamları birden çok kaynak sunucuları yayılıyorsa hello v2.0 uç hello ilk kapsamında belirtilen hello kaynak için bir belirteç döndürür.  Kapsamları hakkında daha ayrıntılı açıklaması için çok başvuran[izinleri, onay ve kapsamları](active-directory-v2-scopes.md). |
| refresh_token |Gerekli |Merhaba akışının hello ikinci leg aldığınız hello refresh_token. |
| redirect_uri |Gerekli |kullanılan tooacquire hello authorization_code olduğu aynı redirect_uri değeri hello. |
| client_secret |Web uygulamaları için gerekli |Merhaba uygulama kayıt Portalı'nda uygulamanız için oluşturduğunuz hello uygulama gizli anahtarı.  Client_secrets güvenilir bir şekilde cihazlarda depolanamaz çünkü yerel bir uygulamada kullanılmamalıdır.  Web uygulamaları ve web hello özelliği toostore hello client_secret güvenli bir şekilde hello sunucu tarafında sahip API'leri için gereklidir. |

#### Başarılı yanıt
Başarılı bir token yanıt gibi görünür:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parametre | Açıklama |
| --- | --- |
| access_token |Merhaba istenen erişim belirteci. Merhaba uygulaması web API'si gibi kaynak güvenli Bu belirteci tooauthenticate toohello kullanabilir. |
| token_type |Merhaba belirteç türü değeri gösterir. Hello Azure AD destekleyen türü olan taşıyıcı |
| expires_in |Ne kadar süreyle hello erişim belirteci (saniye olarak) geçerli değil. |
| Kapsam |access_token hello hello kapsamlar için geçerlidir. |
| refresh_token |Yeni bir OAuth 2.0 yenileme belirteci. Merhaba eski yenileme değiştirmelisiniz bu yeni alınan yenileme belirteci tooensure ile belirteci, yenileme belirteçleri mümkün olduğunca uzun bir süredir geçerli kalır. |
| id_token |Bir imzasız JSON Web Token (JWT). Merhaba uygulama can base64Url açtığınız hello kullanıcının bu belirteci toorequest bilgilerini hello kesimleri kodunu çözer. Hello uygulama hello değerleri önbelleğe ve bunları görüntüler, ancak, bunlar üzerinde herhangi bir yetkilendirme veya güvenlik sınırları için güvenmemelisiniz.  Merhaba id_tokens hakkında daha fazla bilgi için bkz: [v2.0 uç noktası belirteç başvurusu](active-directory-v2-tokens.md). |

#### Hata yanıtı
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| error_codes |Tanılamada yardımcı olabilecek STS belirli hata kodlarının listesi. |
| timestamp |Merhaba hata gerçekleştiği hello süre. |
| trace_id |Tanılamada yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |
| correlation_id |Tanılama'bileşenlerinde yardımcı olabilecek hello isteği için benzersiz bir tanımlayıcı. |

Merhaba hata kodları ve önerilen istemci eylem hello açıklaması için lütfen bkz [belirteç uç noktası hataları için hata kodları](#error-codes-for-token-endpoint-errors).

