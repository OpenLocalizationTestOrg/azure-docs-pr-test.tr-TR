---
title: "Hello Azure AD v2.0 örtük akışını kullanarak aaaSecure tek sayfa uygulamaları | Microsoft Docs"
description: "Tek sayfa uygulamaları için Azure AD v2.0 uygulaması hello örtük akışını kullanarak web uygulamaları oluşturma."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# v2.0 protokolleri - hello örtük akışını kullanarak SPAs
Merhaba v2.0 uç noktası ile kullanıcılar, tek sayfa uygulamaları Microsoft'tan hem kişisel hem de iş/Okul hesaplarıyla içine imzalayabilirsiniz.  Tek sayfa ve ilgi çekici birkaç sınar öncelikle bir tarayıcı karşılaştıkları çalışan diğer JavaScript uygulamaları tooauthentication gelir:

* Bu uygulamaları Hello güvenlik özelliklerini tabanlı geleneksel sunucu web uygulamalarından önemli ölçüde farklıdır.
* Çok sayıda yetkilendirme sunucularını & kimlik sağlayıcıları CORS isteklerini desteklemez.
* Tam sayfa tarayıcı yeniden yönlendirmeleri hello uygulama çıktığınızda özellikle bozucu toohello kullanıcı deneyimi olur.

Bu uygulamalar için (düşünün: AngularJS, Ember.js, React.js, vb.) Azure AD hello OAuth 2.0 örtük verme akış destekler.  Merhaba örtük akış hello açıklanan [OAuth 2.0 belirtimi](http://tools.ietf.org/html/rfc6749#section-4.2).  Birincil avantajı, hello uygulama tooget belirteçleri Azure AD'den bir arka uç sunucu kimlik bilgileri değişimi yapmadan olanak sağlamasıdır.  Bu hello uygulama toosign hello kullanıcı sağlar, oturumu korumak ve hello istemci JavaScript kodu içindeki tüm belirteçleri tooother web API'leri elde edin.  Merhaba örtük akış - özellikle yaklaşık kullanırken dikkate birkaç önemli güvenlik konuları tootake olan [istemci](http://tools.ietf.org/html/rfc6749#section-10.3) ve [kullanıcı kimliğine bürünme özelliğini](http://tools.ietf.org/html/rfc6749#section-10.3).

Toouse hello örtük akış ve Azure AD tooadd kimlik doğrulaması tooyour JavaScript uygulaması isterseniz, bizim açık kaynak JavaScript Kitaplığı kullanmanız önerilir [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Birkaç AngularJS öğreticileri kullanılabilir [burada](active-directory-appmodel-v2-overview.md#getting-started) başlamanıza toohelp.  

Ancak, siz toouse bir kitaplık tek sayfa uygulaması ve gönderme Protokolü iletilerinizi kendiniz tercih ediyorsanız, hello genel adımları izleyin.

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

## Protokol diyagramı
Merhaba akışındaki tüm örtük oturum şuna benzer - hello adımların her biri aşağıda ayrıntılı olarak açıklanmıştır.

![Openıd Connect kulvarları](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Merhaba oturum açma isteği gönder
tooinitially oturum hello kullanıcı uygulamanıza gönderebilirsiniz bir [Openıd Connect](active-directory-v2-protocols-oidc.md) yetkilendirme isteği ve get bir `id_token` hello v2.0 uç noktasından:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Bu istek tooexecute Hello bağlantıya tıklayın! Oturum açtıktan sonra tarayıcınızı çok yeniden yönlendirilmesi gereken`https://localhost/myapp/` ile bir `id_token` hello adres çubuğundaki.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://Login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: `common`, `organizations`, `consumers`ve Kiracı tanımlayıcıları.  Daha fazla ayrıntı için [protokol Temelleri](active-directory-v2-protocols.md#endpoints). |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello kayıt portalı ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) uygulamanızı atanmış. |
| response_type |Gerekli |İçermelidir `id_token` Openıd Connect oturum açma için.  Merhaba response_type içerebilir `token`. Kullanarak `token` bir erişim belirtecinden hemen hello kimlik doğrulama uç noktası toomake ikinci bir istek toohello yetkilendirmek zorunda kalmadan, uygulama tooreceive burada sağlayacak uç noktası.  Merhaba kullanırsanız `token` response_type, hello `scope` parametresi için hangi kaynak tooissue hello belirteci belirten bir kapsam içermesi gerekir. |
| redirect_uri |Önerilen |Burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan, uygulamanızın Hello redirect_uri.  Bu tam olarak bir url kodlanmış olmalıdır dışında hello Portalı'nda kayıtlı hello redirect_uris eşleşmelidir. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi.  Openıd Connect için bunu hello kapsamını içermelidir `openid`, toohello "oturum" iznini hello izin UI çevirir.  İsteğe bağlı olarak da tooinclude hello isteyebilirsiniz `email` veya `profile` [kapsamları](active-directory-v2-scopes.md) erişim tooadditional kullanıcı verilerini öğrenilmesi.  Bu isteği onay toovarious kaynakları isteyen diğer kapsamları ekleyebiliriz. |
| response_mode |Önerilen |Kullanılan toosend hello elde edilen belirteci geri tooyour uygulama olmalıdır hello yöntemini belirtir.  Olmalıdır `fragment` hello örtük akış için. |
| durum |Önerilen |Hello belirteci yanıt olarak da döndürülür hello istekte bulunan bir değer.  İstediğiniz herhangi bir içerik dizesi olabilir.  Rastgele oluşturulan benzersiz bir değer tipik olarak kullanılan [siteler arası istek sahteciliğini saldırılarını önleme](http://tools.ietf.org/html/rfc6749#section-10.12).  hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |
| nonce |Gerekli |Merhaba elde edilen id_token bir talep olarak dahil edilecek hello uygulama tarafından üretilen hello isteğinde bulunan bir değer.  Merhaba uygulama daha sonra bu değeri toomitigate belirteç yeniden yürütme saldırılarına doğrulayabilirsiniz.  Merhaba genellikle kullanılan tooidentify hello kaynak hello isteğinin olabilir rastgele, benzersiz bir dize değeridir. |
| istemi |İsteğe bağlı |Gerekli bir kullanıcı etkileşimi Hello türünü belirtir.  Yalnızca şu anda geçerli değerler 'oturum açma', 'none' hello ve 'onay'.  `prompt=login`zorla kullanıcı tooenter üzerinde çoklu oturum negating bu isteğin kimlik bilgilerini hello.  `prompt=none`Ters hello - hello kullanıcının hiçbir etkileşimli istemi doğabilecek sunulmayan sağlayacak olur.  Merhaba isteği sessizce çoklu oturum açma aracılığıyla tamamlanamazsa, hello v2.0 uç noktası bir hata döndürür.  `prompt=consent`Tetikleyici hello OAuth hello kullanıcı toogrant izinleri toohello uygulama soran iletişim hello kullanıcı işaretleri, sonra onay. |
| login_hint |İsteğe bağlı |Olması kullanılan toopre dolgu hello kullanıcı adı/e-posta adresi alanı hello uygulamasında oturum açabilir sayfa hello kullanıcı için kullanıcı adı önceden biliyorsanız.  Bir önceki oturum bileşeninden hello kullanıcı adı zaten ayıklanan yeniden kimlik doğrulaması sırasında bu parametre genellikle uygulamaları kullanacak hello kullanarak `preferred_username` talep. |
| domain_hint |İsteğe bağlı |Aşağıdakilerden biri olabilir `consumers` veya `organizations`.  Dahil edilmişse, hello e-posta tabanlı bulma işlemi atlar kullanıcı hello v2.0 oturum açma sayfası, üzerinde önde gelen tooa biraz daha verimli bir kullanıcı deneyimi geçtiği.  Genellikle uygulamaları kullanacağınız Bu parametre yeniden kimlik doğrulaması sırasında hello çıkartarak `tid` hello id_token talep.  Merhaba, `tid` değer talep `9188040d-6c67-4c5b-b112-36a304b66dad`, kullanmanız gereken `domain_hint=consumers`.  Aksi takdirde kullanın `domain_hint=organizations`. |

Bu noktada, hello kullanıcı olacaktır tooenter kendi kimlik bilgilerini ve tam hello kimlik doğrulaması istedi.  Hello v2.0 uç noktası da o hello kullanıcı hello belirtilen toohello izinleri rıza sağlayacak `scope` sorgu parametresi.  Merhaba kullanıcı tooany bu izin verdiği değil, bu hello kullanıcı tooconsent toohello gerekli izinleri sorar.  Ayrıntılarını [izinleri, onay ve çok kiracılı uygulamalara sağlanan burada](active-directory-v2-scopes.md).

Merhaba kullanıcı kimliğini doğrular ve izin veren sonra hello v2.0 uç hello belirtilen bir yanıt tooyour uygulamaya döndürülecek `redirect_uri`, hello belirtilen hello yöntemi kullanarak `response_mode` parametresi.

#### Başarılı yanıt
Başarılı yanıt kullanarak `response_mode=fragment` ve `response_type=id_token+token` okunabilirliği için satır sonu ile Merhaba aşağıdaki gibi görünür:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Parametre | Açıklama |
| --- | --- |
| access_token |Eklenen IF `response_type` içeren `token`. İstenen uygulama hello hello erişim belirteci bu durumda için hello Microsoft Graph.  Hello erişim belirteci kodunu çözdü veya aksi halde Denetlenmekte, genel olmayan bir dize olarak işlenebilir. |
| token_type |Eklenen IF `response_type` içeren `token`.  Her zaman açık `Bearer`. |
| expires_in |Eklenen IF `response_type` içeren `token`.  Merhaba hello belirteci amacıyla önbelleğe alma için geçerli kaldığı saniye sayısını gösterir. |
| Kapsam |Eklenen IF `response_type` içeren `token`.  Merhaba kapsamlar için hangi hello access_token geçerli olacağını belirtir. |
| id_token |İstenen uygulama hello hello id_token. Merhaba kullanıcıyla oturumu başlatmak ve hello id_token tooverify hello kullanıcının kimliğini kullanın.  İd_tokens ve içerikleri hakkında daha fazla ayrıntı hello dahil [v2.0 uç noktası belirteç başvurusu](active-directory-v2-tokens.md). |
| durum |Bir durum parametresi hello istekte yer alıyorsa hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama hello durum değerleri hello istek ve yanıtta özdeş olduğunu doğrulamanız gerekir. |

#### Hata yanıtı
Hata yanıtları toohello da gönderilebilir `redirect_uri` hello uygulama bunları uygun şekilde işleyebilmesi için:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

## Merhaba id_token doğrula
Yalnızca bir id_token alma yeterli tooauthenticate hello kullanıcı değildir; Merhaba id_token'ın imzayı doğrulamak ve uygulamanızın gereksinimleri başına hello belirtecindeki hello talep doğrulamanız gerekir.  Merhaba v2.0 uç noktası kullanan [JSON Web belirteçleri (Jwt'ler)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) ve ortak anahtar şifrelemesi toosign belirteçleri ve geçerli olduğunu doğrulayın.

Toovalidate hello seçebilirsiniz `id_token` istemci kodda, ancak toosend hello yaygın bir uygulamadır `id_token` tooa arka uç sunucusuna ve hello doğrulama gerçekleştirin.  Merhaba id_token hello imzası doğruladıktan sonra gerekli tooverify olacak birkaç talep vardır.  Hello bkz [v2.0 belirteç başvurusu](active-directory-v2-tokens.md) daha fazla bilgi dahil olmak üzere [doğrulama belirteçleri](active-directory-v2-tokens.md#validating-tokens) ve [önemli bilgiler hakkında imzalama anahtarı Rollover](active-directory-v2-tokens.md#validating-tokens).  Öneririz ayrıştırma ve doğrulama yapmayı kullanımını kitaplık belirteçler - en az bir olduğundan çoğu diller ve platformlar için kullanılabilir.
<!--TODO: Improve hello information on this-->

Ayrıca, ek talep senaryonuza bağlı olarak toovalidate isteyebilir.  Bazı ortak doğrulamaları şunları içerir:

* Merhaba kullanıcı/kuruluş sağlama hello uygulaması için kaydolmuş.
* Sağlama hello kullanıcının uygun yetkilendirme/ayrıcalıklara sahip
* Belirli bir kimlik doğrulama gücünü sağlayarak, çok faktörlü kimlik doğrulaması gibi oluştu.

Merhaba bir id_token hello Taleplerde hakkında daha fazla bilgi için bkz: [v2.0 uç noktası belirteç başvurusu](active-directory-v2-tokens.md).

Merhaba id_token tamamen doğruladıktan sonra hello kullanıcı bir oturumla başlar ve hello talep hello id_token tooobtain kullanma hakkında bilgi hello kullanıcı uygulamanızı.  Bu bilgiler kullanılabilir ekran kayıtları, yetkilerini, vb. için.

## Erişim belirteci alın
Tek sayfa uygulamanıza hello kullanıcı oturum açtığınız, çağrıyı yapan web API'leri gibi hello Azure AD tarafından güvenli hale getirilmiş için erişim belirteçleri elde edebilirsiniz [Microsoft Graph](https://graph.microsoft.io).  Hello kullanarak bir belirteç zaten alınmış olsa bile `token` response_type, tooredirect hello kullanıcı toosign yeniden vermeden bu yöntem tooacquire belirteçleri tooadditional kaynakları kullanabilir.

Merhaba normal Openıd Connect/OAuth akışında bir istek toohello v2.0 yaparak bunu `/token` uç noktası.  Ancak, hello v2.0 uç AJAX yapma tooget çağırır yenileme belirteçleri hello soru dışında böylelikle değil destek CORS isteklerini desteklemez.  Bunun yerine, diğer web API'leri gizli IFRAME tooget yeni belirteçlerinde hello örtük akış kullanabilirsiniz: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> & Hello isteği aşağıda bir tarayıcı sekmesi yapıştırma Kopyala deneyin! (Tooreplace hello unutmayın `domain_hint` ve hello `login_hint` hello değerlerle kullanıcınız için değerleri düzeltin)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: `common`, `organizations`, `consumers`ve Kiracı tanımlayıcıları.  Daha fazla ayrıntı için [protokol Temelleri](active-directory-v2-protocols.md#endpoints). |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello kayıt portalı ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) uygulamanızı atanmış. |
| response_type |Gerekli |İçermelidir `id_token` Openıd Connect oturum açma için.  Bu ayrıca diğer response_types gibi içerebilir `code`. |
| redirect_uri |Önerilen |Burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan, uygulamanızın Hello redirect_uri.  Bu tam olarak bir url kodlanmış olmalıdır dışında hello Portalı'nda kayıtlı hello redirect_uris eşleşmelidir. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi.  Belirteçleri almak için tüm dahil [kapsamları](active-directory-v2-scopes.md) için hello kaynak ilgi gerektirir. |
| response_mode |Önerilen |Kullanılan toosend hello elde edilen belirteci geri tooyour uygulama olmalıdır hello yöntemini belirtir.  Aşağıdakilerden biri olabilir `query`, `form_post`, veya `fragment`. |
| durum |Önerilen |Hello belirteci yanıt olarak da döndürülür hello istekte bulunan bir değer.  İstediğiniz herhangi bir içerik dizesi olabilir.  Rastgele oluşturulan benzersiz bir değer genellikle siteler arası istek sahteciliği saldırılarına önlemek için kullanılır.  hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |
| nonce |Gerekli |Merhaba elde edilen id_token bir talep olarak dahil edilecek hello uygulama tarafından üretilen hello isteğinde bulunan bir değer.  Merhaba uygulama daha sonra bu değeri toomitigate belirteç yeniden yürütme saldırılarına doğrulayabilirsiniz.  Merhaba genellikle kullanılan tooidentify hello kaynak hello isteğinin olabilir rastgele, benzersiz bir dize değeridir. |
| istemi |Gerekli |Yenileme & içinde gizli bir iframe belirteçleri almak için kullanmanız gereken `prompt=none` IFRAME hello tooensure hello v2.0 oturum açma sayfası üzerinde askıda değil ve hemen döndürür. |
| login_hint |Gerekli |Yenileme & içinde gizli bir iframe belirteçleri almak için sipariş toodistinguish hello kullanıcı belirli bir anda zamanında olabilir birden çok oturumlar arasında bu ipucunda hello kullanıcının kullanıcı adı hello eklemeniz gerekir. Bir önceki oturum bileşeninden hello kullanıcıadı ayıklayabilirsiniz hello kullanarak `preferred_username` talep. |
| domain_hint |Gerekli |Aşağıdakilerden biri olabilir `consumers` veya `organizations`.  Yenileme & içinde gizli bir iframe belirteçleri almak için hello istekte hello domain_hint eklemeniz gerekir.  Merhaba ayıklamak `tid` hangi değer toouse önceki bir oturum açma toodetermine hello id_token talep.  Merhaba, `tid` değer talep `9188040d-6c67-4c5b-b112-36a304b66dad`, kullanmanız gereken `domain_hint=consumers`.  Aksi takdirde kullanın `domain_hint=organizations`. |

Teşekkürler toohello `prompt=none` parametresi, bu istek ya da başarılı ya da hemen başarısız olacak ve dönüş tooyour uygulama.  Başarılı yanıt tooyour uygulama belirtilen hello gönderilecek `redirect_uri`, hello belirtilen hello yöntemi kullanarak `response_mode` parametresi.

#### Başarılı yanıt
Başarılı yanıt kullanarak `response_mode=fragment` gibi görünüyor:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| Parametre | Açıklama |
| --- | --- |
| access_token |İstenen uygulama hello hello belirteci. |
| token_type |Her zaman açık `Bearer`. |
| durum |Bir durum parametresi hello istekte yer alıyorsa hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama hello durum değerleri hello istek ve yanıtta özdeş olduğunu doğrulamanız gerekir. |
| expires_in |Ne kadar süreyle hello erişim belirteci (saniye olarak) geçerli değil. |
| Kapsam |erişim belirteci hello hello kapsamlar için geçerlidir. |

#### Hata yanıtı
Hata yanıtları toohello da gönderilebilir `redirect_uri` hello uygulama bunları uygun şekilde işleyebilmesi için.  Merhaba durumda `prompt=none`, beklenen hata olacaktır:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

Merhaba IFRAME istekte bu hatayı alırsanız hello kullanıcı etkileşimli olarak yeniden tooretrieve içinde yeni bir belirteç oturum açmanız gerekir.  Bu durumda toohandle yolu, uygulamanız için mantıklı de seçebilirsiniz.

## Yenileme belirteçleri
Her ikisi de `id_token`s ve `access_token`s kısa bir süre sonra dolacak, uygulamanızı toorefresh hazırlanması gerekir böylece bu belirteçler düzenli aralıklarla.  belirteci yazın ya da toorefresh hello gerçekleştirebilir hello kullanarak yukarıdaki aynı gizli IFRAME isteği `prompt=none` parametresi toocontrol Azure AD davranışı.  Yeni bir tooreceive istiyorsanız `id_token`, emin toouse olması `response_type=id_token` ve `scope=openid`, yanı sıra bir `nonce` parametresi.

## Bir oturum kapatma isteği gönder
Merhaba Openıdconnect `end_session_endpoint` bir kullanıcının oturumunu ve Temizle tanımlama bilgilerini ayarlama hello v2.0 uç noktası tarafından bir istek toohello v2.0 uç noktası tooend uygulama toosend sağlar.  toofully oturum bir web uygulaması dışında bir kullanıcı, uygulamanız (genellikle bir belirteç önbelleği temizlemek veya tanımlama bilgilerini silmek) hello kullanıcıyla kendi oturumunu sona erdirme ve hello tarayıcıya yönlendirin:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: `common`, `organizations`, `consumers`ve Kiracı tanımlayıcıları.  Daha fazla ayrıntı için [protokol Temelleri](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | Önerilen | Kullanıcı hello hello URL tooafter oturum kapatma tamamlandıktan döndürülmelidir. Bu değer URI'ler hello uygulama için kayıtlı hello yeniden yönlendirme biriyle eşleşmelidir. Dahil edilmezse, hello kullanıcı hello v2.0 uç noktası tarafından genel bir ileti gösterilir. |
