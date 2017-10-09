---
title: "Active Directory v2.0 ve hello Openıd Connect Protokolü aaaAzure | Microsoft Docs"
description: "Web uygulamaları hello Azure AD v2.0 uygulama hello Openıd Connect kimlik doğrulama protokolü kullanarak oluşturun."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 ve hello Openıd Connect Protokolü
Openıd Connect OAuth 2.0 kullanıcı tooa web uygulamasında toosecurely oturum kullanabileceğiniz yerleşik bir kimlik doğrulama protokolüdür. Openıd Connect hello v2.0 uç noktanın uygulamasını kullandığınızda, oturum açma ve API erişim tooyour web tabanlı uygulamalar ekleyebilirsiniz. Bu makalede, nasıl gösteriyoruz toodo bu dilden bağımsız. Biz açıklamak nasıl toosend ve tüm Microsoft açık kaynak kitaplıkları kullanmadan HTTP iletileri alabilirsiniz.

> [!NOTE]
> Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez. mı hello v2.0 uç kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

[Openıd Connect](http://openid.net/specs/openid-connect-core-1_0.html) hello OAuth 2.0 genişletir *yetkilendirme* Protokolü toouse olarak bir *kimlik doğrulaması* tek gerçekleştirebilmeleri için protokol OAuth kullanılarak oturum. Openıd Connect hello kavramını sunmaktadır bir *kimliği belirteci*, tooverify hello hello kullanıcının kimliğini hello istemci izin veren bir güvenlik belirteci değil. Hello kimliği belirteci ayrıca hello kullanıcının temel profil bilgilerini alır. Openıd Connect OAuth 2.0 genişlettiğinden uygulamaları güvenli bir şekilde elde edebilirsiniz *erişim belirteçleri*, tarafından güvenliği sağlanan kullanılan tooaccess kaynakları olabilen bir [yetkilendirme sunucusu](active-directory-v2-protocols.md#the-basics). Oluşturmakta olduğunuz Openıd Connect kullanmanızı öneririz bir [web uygulaması](active-directory-v2-flows.md#web-apps) bir sunucuda barındırılan ve tarayıcı yoluyla erişilir.

## Protokol diyagramı: oturum açma
Merhaba oturum açma en temel akış hello sonraki diyagramda gösterildiği hello adım vardır. Biz bu makalede ayrıntılı her adım açıklanmaktadır.

![Openıd Connect protokolü: oturum açma](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Merhaba Openıd Connect meta veri belgesi getirme
Openıd Connect bir uygulama tooperform oturum açma için gerekli hello bilgilerin çoğunu içeren bir meta veri belgesi açıklar. Bu hello URL'leri toouse ve hello hizmetin ortak İmzalama anahtarları hello konumunu gibi bilgileri içerir. Merhaba v2.0 uç noktası için bu meta veri belgesi Openıd Connect hello kullanmanız gerekir.

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Merhaba `{tenant}` dört değerden birini alabilir:

| Değer | Açıklama |
| --- | --- |
| `common` |Kullanıcıların kişisel bir Microsoft hesabı ve bir iş veya Okul hesabı Azure Active Directory (Azure AD) ile toohello uygulamada oturum açabilir. |
| `organizations` |Yalnızca kullanıcılarla iş veya Okul hesapları Azure AD'den toohello uygulamada oturum açabilirsiniz. |
| `consumers` |Yalnızca kişisel bir Microsoft hesabı olan kullanıcılar toohello uygulamada oturum açabilir. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` veya `contoso.onmicrosoft.com` |Yalnızca kullanıcıların belirli bir Azure AD'den bir iş veya Okul hesabıyla Kiracı toohello uygulamada oturum açabilirsiniz. Merhaba kolay etki alanı adını Azure AD kiracısı hello ya da hello kiracının GUID tanımlayıcısı kullanılabilir. |

Basit bir JavaScript nesne gösterimi (JSON) belge Hello meta verilerdir. Aşağıdaki kod parçacığında bir örnek hello bakın. Merhaba parçacığı'nin içeriği tam olarak hello açıklanan [Openıd Connect belirtimi](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

Genellikle, bu meta veri belgesi tooconfigure Openıd Connect kitaplığı veya SDK kullanırsınız; Merhaba kitaplığı hello meta veri toodo çalışmasını kullanırsınız. Ancak, Openıd Connect oluşturma öncesi kitaplığı kullanmıyorsanız hello v2.0 uç kullanarak hello geri kalanında bu makale tooperform oturum açma web uygulamasında hello adımları izleyebilirsiniz.

## Merhaba oturum açma isteği gönder
Web uygulamanızı tooauthenticate hello kullanıcı gerektiğinde Merhaba kullanıcı toohello yönlendirebilirsiniz `/authorize` uç noktası. Bu istek benzer toohello ilk Bacak hello için olan [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols-oauth-code.md), bu önemli farklılıkları ile:

* Merhaba isteği hello içermelidir `openid` hello kapsamda `scope` parametresi.
* Merhaba `response_type` parametre içermelidir `id_token`.
* Merhaba isteği hello içermelidir `nonce` parametresi.

Örneğin:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Bağlantı tooexecute aşağıdaki hello bu istek'i tıklatın. Oturum açtıktan sonra tarayıcınızı hello adres çubuğundaki kimliği belirteci ile yeniden yönlendirilen toohttps://localhost/myapp/ olacaktır. Bu istek kullanan Not `response_mode=query` (yalnızca tanıtım amacıyla). Kullanmanızı öneririz `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://Login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parametre | Koşul | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba kullanabilirsiniz `{tenant}` toohello uygulamada oturum açan hello isteği toocontrol hello yolunda değeri. Merhaba izin verilen değerler: `common`, `organizations`, `consumers`ve Kiracı tanımlayıcıları. Daha fazla bilgi için bkz: [protokol Temelleri](active-directory-v2-protocols.md#endpoints). |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour uygulama atanmış. |
| response_type |Gerekli |İçermelidir `id_token` Openıd Connect oturum açma için. Bu ayrıca diğer içerebilir `response_types` gibi değerler `code`. |
| redirect_uri |Önerilen |Merhaba burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan uygulamanızı URI'sini yeniden yönlendir. Bu tam olarak hello yeniden yönlendirme URL'si olmalıdır ancak bu hello Portalı'nda kayıtlı URI'ler kodlanmış biriyle eşleşmelidir. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi. Openıd Connect için bunu hello kapsamını içermelidir `openid`, toohello "oturum" iznini hello izin UI çevirir. Bu isteği onay isteyen diğer kapsamları de içerebilir. |
| nonce |Gerekli |Hello sonuç id_token değeri bir talep olarak dahil edilecek hello uygulama tarafından üretilen hello isteğinde bulunan bir değer. Bu değer toomitigate belirteç yeniden yürütme saldırılarına Hello uygulama doğrulayabilirsiniz. Merhaba genellikle kullanılan tooidentify hello kaynak hello isteğinin olabilir rastgele, benzersiz bir dize değeridir. |
| response_mode |Önerilen |Kullanılan toosend hello elde edilen yetkilendirme kodu geri tooyour uygulama olmalıdır hello yöntemini belirtir. Aşağıdakilerden biri olabilir `query`, `form_post`, veya `fragment`. Web uygulamaları için kullanılmasını öneririz `response_mode=form_post`, tooensure hello belirteçleri tooyour uygulamanın en güvenli aktarımı. |
| durum |Önerilen |Merhaba, aynı zamanda isteğinde bir değer hello belirteci yanıt olarak döndürülür. İstediğiniz herhangi bir içerik dizesi olabilir. Rastgele oluşturulmuş bir benzersiz değer genellikle çok kullanılır[siteler arası istek sahteciliği saldırılarına engellemek](http://tools.ietf.org/html/rfc6749#section-10.12). Merhaba kimlik doğrulama isteği oluşmadan önce hello sayfa veya Görünüm hello kullanıcı açıktı gibi hello ayrıca hello kullanıcı durumunun hello uygulamasında kullanılan tooencode bilgilerini durumudur. |
| istemi |İsteğe bağlı |Gerekli bir kullanıcı etkileşimi Hello türünü belirtir. Merhaba şu anda yalnızca geçerli değerler: `login`, `none`, ve `consent`. Merhaba `prompt=login` zorlar hello kullanıcı tooenter kullanıcıların kimlik bilgilerini çoklu oturum açma üzerindeki geçersiz kılar, istek üzerine talep. Merhaba `prompt=none` talep hello ters olduğu. Bu talep hello kullanıcının hiçbir etkileşimli istemi doğabilecek sunulmayan sağlar. Merhaba isteği sessizce çoklu oturum açma tamamlanamazsa, hello v2.0 uç noktası bir hata döndürür. Merhaba `prompt=consent` Tetikleyicileri hello OAuth onay iletişim hello kullanıcı oturum açtıktan sonra talep. Merhaba iletişim hello kullanıcı toogrant izinleri toohello uygulama ister. |
| login_hint |İsteğe bağlı |Önceden hello kullanıcı adını biliyorsanız, bu parametre toopre dolgu hello kullanıcı adı ve e-posta adresi alanı hello oturum açma sayfasının hello kullanıcı için kullanabilirsiniz. Genellikle, uygulamaları zaten hello kullanıcı adı bir önceki oturum bileşeninden hello kullanarak ayıklama sonra yeniden kimlik doğrulaması sırasında bu parametreyi kullanın `preferred_username` talep. |
| domain_hint |İsteğe bağlı |Bu değer `consumers` veya `organizations`. Dahil edilmişse, hello e-posta tabanlı bulma işlemi atlanıyor hello v2.0 oturum açma sayfasında biraz daha kolay bir kullanıcı deneyimi hello kullanıcı geçtiği. Genellikle, uygulamaların bu parametreyi yeniden kimlik doğrulaması sırasında hello çıkartarak kullanın `tid` hello kimliği belirtecinden talep. Merhaba, `tid` değer talep `9188040d-6c67-4c5b-b112-36a304b66dad`, kullanmak `domain_hint=consumers`. Aksi takdirde kullanın `domain_hint=organizations`. |

Bu noktada, hello kullanıcı tam hello kimlik doğrulama ve kimlik bilgileri istendiğinde tooenter değil. Merhaba v2.0 uç hello kullanıcı hello belirtilen toohello izin verdiği doğrular `scope` sorgu parametresi. Merhaba kullanıcı tooany bu izin verdiği değil, hello v2.0 uç hello kullanıcı tooconsent toohello gerekli izinleri ister. Daha fazla bilgi edinebilirsiniz [izinleri, onay ve çok müşterili uygulamalar](active-directory-v2-scopes.md).

Merhaba kullanıcı kimliğini doğrular ve izin veren sonra bir yanıt tooyour uygulamaya hello belirtilen hello v2.0 uç noktası döndürür hello belirtilen hello yöntemi kullanarak yeniden yönlendirme URI'si `response_mode` parametresi.

### Başarılı yanıt
Başarılı yanıt kullandığınızda `response_mode=form_post` şöyle görünür:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parametre | Açıklama |
| --- | --- |
| id_token |İstenen uygulama hello kimliği belirteci hello. Merhaba kullanabilirsiniz `id_token` parametresi tooverify kullanıcının kimliğini hello ve hello kullanıcı bir oturumla başlayın. Merhaba kimlik belirteçlerini ve içerikleri hakkında daha fazla ayrıntı için bkz: [v2.0 uç belirteçler başvuru](active-directory-v2-tokens.md). |
| durum |Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama hello durum değerleri hello istek ve yanıtta özdeş olduğunu doğrulamanız gerekir. |

### Hata yanıtı
Böylece Hello uygulama bunları işleyebilir hata yanıtları toohello yeniden yönlendirme URI'si da gönderilebilir. Bir hata yanıtı şuna benzer:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametre | Açıklama |
| --- | --- |
| error |Tooclassify türlerini oluşan hataları ve tooreact tooerrors kullanabileceğiniz bir hata kodu dizesi. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

### Yetkilendirme uç noktası hataları için hata kodları
Merhaba aşağıdaki tabloda açıklanmaktadır hello döndürülen hata kodlarını `error` hello hata yanıtı parametresinin:

| Hata kodu | Açıklama | İstemci eylemi |
| --- | --- | --- |
| invalid_request |Protokol hatası, bir eksik gibi parametresi gereklidir. |Düzeltin ve hello isteği yeniden gönderin. Bu genellikle ilk test sırasında yakalanan geliştirme hatasıdır. |
| unauthorized_client |Merhaba istemci uygulaması bir yetkilendirme kodu isteğinde bulunamaz. |Bu durum genellikle, Merhaba istemci uygulaması Azure AD'de kayıtlı değil veya toohello kullanıcının Azure AD kiracısı eklenmez genellikle ortaya çıkar. Merhaba uygulaması yönergeleri tooinstall hello uygulamayla hello kullanıcıdan ve tooAzure AD ekleyin. |
| ACCESS_DENIED |Merhaba kaynak sahibi izni reddedildi. |Merhaba istemci uygulaması hello kullanıcı izin sürece devam edemiyor hello kullanıcı bildirebilir. |
| unsupported_response_type |Merhaba yetkilendirme sunucusu hello istekte hello yanıt türünü desteklemiyor. |Düzeltin ve hello isteği yeniden gönderin. Bu genellikle ilk test sırasında yakalanan geliştirme hatasıdır. |
| server_error |Merhaba sunucu beklenmeyen bir hatayla karşılaştı. |Merhaba isteği yeniden deneyin. Bu hatalar geçici koşulları neden olabilir. Merhaba istemci uygulaması toohello kullanıcı açıklayan yanıt tooa geçici hata ertelendi. |
| temporarily_unavailable |Merhaba geçici olarak meşgul toohandle hello isteği sunucusudur. |Merhaba isteği yeniden deneyin. Merhaba istemci uygulaması toohello kullanıcı açıklayan yanıt tooa geçici koşul ertelendi. |
| invalid_resource |Merhaba hedef kaynak mevcut değil, Azure AD, bulunamıyor veya düzgün yapılandırılmamış için geçersiz. |Bu, varsa, hello kaynak hello Kiracı yapılandırılmadı olduğunu gösterir. Merhaba uygulaması, hello kullanıcıdan hello uygulama yükleme ve tooAzure AD eklemek için yönergeler de. |

## Merhaba kimliği belirtecini doğrula
Bir kimliği belirteci alma yeterli tooauthenticate hello kullanıcı değil. Ayrıca hello kimliği belirtecin imzayı doğrulamak ve uygulamanızın gereksinimleri başına hello belirtecindeki hello talep doğrulamanız gerekir. Merhaba v2.0 uç noktası kullanan [JSON Web belirteçleri (Jwt'ler)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) ve ortak anahtar şifrelemesi toosign belirteçleri ve geçerli olduğunu doğrulayın.

İstemci kodu toovalidate hello kimliği belirteci seçebilirsiniz, ancak ortak bir uygulama toosend hello kimliği belirteci tooa arka uç sunucusu ve hello doğrulama gerçekleştirin. Merhaba kimliği belirtecinin imzası hello doğruladıktan sonra birkaç talep tooverify gerekir. Daha fazla bilgi için daha fazla dahil olmak üzere [belirteçleri doğrulama](active-directory-v2-tokens.md#validating-tokens) ve [anahtar geçişi imzalama hakkında önemli bilgiler](active-directory-v2-tokens.md#validating-tokens), hello bkz [v2.0 belirteçler başvuru](active-directory-v2-tokens.md). Biz kitaplığı tooparse kullanmanız önerilir ve belirteçleri doğrulamak. Bu kitaplıklar en az biri çoğu diller ve platformlar için mevcut değil.
<!--TODO: Improve hello information on this-->

Senaryonuza bağlı olarak toovalidate ek talepleri de isteyebilirsiniz. Bazı ortak doğrulamaları şunları içerir:

* Merhaba kullanıcıya veya kuruluşa hello uygulaması için kaydolmuş emin olun.
* Merhaba kullanıcı yetkilendirme veya ayrıcalıkları gerekli olun.
* Belirli bir kimlik doğrulama gücü, çok faktörlü kimlik doğrulaması gibi oluştuğunu emin olun.

Merhaba hello talep kimliği belirteci hakkında daha fazla bilgi için bkz: [v2.0 uç belirteçler başvuru](active-directory-v2-tokens.md).

Merhaba kimliği belirteci tamamen doğrulandıktan sonra bir oturum hello kullanıcıyla başlayabilirsiniz. Merhaba talep hello kimliği belirteci tooget kullanma hakkında bilgi, uygulamanızda hello kullanıcı. Görüntü, kayıtları, yetkilerini ve benzeri için bu bilgileri kullanabilirsiniz.

## Oturum kapatma isteği gönder
Uygulamanızdan hello kullanıcı çıkışı toosign istediğinizde, uygulamanızın tanımlama bilgilerini yeterli tooclear değil veya aksi halde hello kullanıcının oturumunu sona erdirmek. Ayrıca hello kullanıcı toohello v2.0 uç noktası toosign giden yönlendirmesi gerekir. Bunu yapmazsanız, geçerli tek bir oturum açma oturumu hello v2.0 uç noktası ile olacağı hello kullanıcı tooyour uygulama kendi kimlik bilgilerini yeniden girmeye gerek kalmadan yeniden kimliğini doğrular.

Merhaba kullanıcı toohello yönlendirebilirsiniz `end_session_endpoint` hello Openıd Connect meta veri belgesinde listelenen:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| Parametre | Koşul | Açıklama |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Önerilen | Kullanıcı hello hello başarıyla oturumunuzu yeniden yönlendirilen tooafter URL'dir. Merhaba parametre dahil edilmezse, hello kullanıcı hello v2.0 uç noktası tarafından oluşturulan genel bir ileti gösterilir. Bu URL hello uygulama kayıt Portalı'nda, uygulamanız için URI kayıtlı hello yeniden yönlendirme biriyle eşleşmelidir.  |

## Çoklu oturum kapatma
Yönlendirme zaman hello kullanıcı toohello `end_session_endpoint`, hello v2.0 uç hello tarayıcı hello kullanıcının oturumunu temizler. Ancak, hello kullanıcı hala Microsoft hesapları için kimlik doğrulaması kullanan tooother uygulamalarda imzalanması. tooenable bu uygulamaları toosign hello kullanıcı aynı anda hello v2.0 uç çıkış gönderir kayıtlı bir HTTP GET isteği toohello `LogoutUrl` tüm hello uygulamalarının hello kullanıcı şu anda oturum. Uygulamalar gerekir yanıt toothis isteği hello kullanıcı ve döndürme tanımlayan herhangi bir oturumunda temizleyerek bir `200` yanıt.  Uygulamanızda toosupport çoklu oturum kapatma istiyorsanız gibi uygulamalıdır bir `LogoutUrl` uygulamanızın kodu.  Merhaba ayarlayabilirsiniz `LogoutUrl` hello uygulama kayıt Portalı'ndan.

## Protokol diyagramı: belirteci edinme
Birçok web uygulamaları, OAuth kullanarak yalnızca oturum hello kullanıcı toonot, aynı zamanda tooaccess hello kullanıcı adına bir web hizmeti gerekir. Bu senaryo, Openıd Connect birleştiren bir yetkilendirme aynı anda alınırken kullanıcı kimlik doğrulaması için hello OAuth yetkilendirme kodu akışını kullanıyorsanız tooget erişim kullanabileceğiniz kod belirteçleri.

tam Openıd Connect oturum açma hello ve belirteç edinme akış benzer toohello sonraki diyagramı görünür. Biz her adım hello makalenin hello sonraki bölümlerde ayrıntılı olarak açıklanmaktadır.

![Openıd Connect protokolü: belirteci edinme](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Erişim belirteci alın
tooacquire erişim belirteçleri, hello oturum açma isteği değiştirin:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Bağlantı tooexecute aşağıdaki hello bu istek'i tıklatın. Oturum açtıktan sonra tarayıcınızı kimliği belirteci ve bir kodla hello adres çubuğundaki yeniden yönlendirilen toohttps://localhost/myapp/ ' dir. Bu istek kullanan Not `response_mode=query` (yalnızca tanıtım amacıyla). Kullanmanızı öneririz `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://Login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

Merhaba isteğindeki ve kullanarak izin kapsamları ekleyerek `response_type=id_token code`, hello v2.0 uç sağlar hello kullanıcı hello belirtilen toohello izin verdiği `scope` sorgu parametresi. Bir erişim belirteci bir yetkilendirme kodu tooyour uygulama tooexchange döndürür.

### Başarılı yanıt
Kullanarak başarılı bir yanıt `response_mode=form_post` şöyle görünür:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parametre | Açıklama |
| --- | --- |
| id_token |İstenen uygulama hello kimliği belirteci hello. Merhaba kullanıcıyla oturumu başlatmak ve hello kimliği belirteci tooverify hello kullanıcının kimliğini kullanın. Hello kimlik belirteçlerini ve içerikleri hakkında daha fazla ayrıntı bulabilirsiniz [v2.0 uç belirteçler başvuru](active-directory-v2-tokens.md). |
| Kod |İstenen uygulama hello hello yetkilendirme kodu. Merhaba uygulama hello yetkilendirme kodu toorequest bir erişim belirteci hello hedef kaynak için kullanabilirsiniz. Bir kimlik doğrulama kodu çok kısa süreli ' dir. Genellikle, bir kimlik doğrulama kodu yaklaşık 10 dakika içinde süresi dolar. |
| durum |Bir durum parametresi hello istekte yer alıyorsa hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama hello durum değerleri hello istek ve yanıtta özdeş olduğunu doğrulamanız gerekir. |

### Hata yanıtı
Böylece Hello uygulama bunları uygun şekilde işleyebilir hata yanıtları toohello yeniden yönlendirme URI'si da gönderilebilir. Bir hata yanıtı şuna benzer:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametre | Açıklama |
| --- | --- |
| error |Tooclassify türlerini oluşan hataları ve tooreact tooerrors kullanabileceğiniz bir hata kodu dizesi. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

Olası hata kodları ve önerilen istemci yanıtları açıklaması için bkz: [yetkilendirme uç noktası hataları için hata kodları](#error-codes-for-authorization-endpoint-errors).

Bir yetkilendirme kodu ve bir kimliği belirtecine sahip olduğunda hello kullanıcı oturum açabilir ve onların adına erişim belirteci alın. toosign hello kullanıcı hello kimliği belirteci doğrulamak gerekir [açıklandığı gibi tam olarak](#validate-the-id-token). tooget erişim belirteçleri, açıklanan başlangıç adımları izleyin bizim [OAuth Protokolü belgeleri](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
