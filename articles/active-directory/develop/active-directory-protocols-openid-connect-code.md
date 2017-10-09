---
title: "aaaUnderstand hello Openıd Connect kimlik doğrulama kodu akışı Azure AD'de | Microsoft Docs"
description: "Bu makalede toouse HTTP iletileri tooauthorize nasıl erişim tooweb uygulamaları ve web API kullanarak Azure Active Directory ve Openıd Connect kiracınızda açıklanmaktadır."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Openıd Connect ve Azure Active Directory kullanılarak erişim tooweb uygulamaları yetkilendirmek
[Openıd Connect](http://openid.net/specs/openid-connect-core-1_0.html) olan hello OAuth 2.0 protokolü en üstünde oluşturulan Basit kimlik katmanı. OAuth 2.0 tanımlar mekanizmaları tooobtain ve kullanım **erişim belirteçleri** tooaccess korumalı kaynakların, ancak standart yöntemleri tooprovide kimlik bilgileri belirtmiyor. Openıd Connect kimlik doğrulama bir uzantı toohello OAuth 2.0 Yetkilendirme işlemi uygular. Merhaba biçiminde hello son kullanıcı hakkında bilgi sağlayan bir `id_token` hello hello kullanıcının kimliğini doğrular ve hello kullanıcının temel profil bilgilerini sağlar.

Bir sunucuda barındırılan ve tarayıcı erişilen bir web uygulaması oluşturuyorsanız Openıd Connect bizim önerilir.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Openıd Connect kullanarak kimlik doğrulama akışı
Merhaba en basit oturum açma akışı hello aşağıdaki adımları içerir - bunların her biri aşağıda ayrıntılı olarak açıklanmıştır.

![Openıd Connect kimlik doğrulama akışı](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Openıd Connect meta veri belgesi

Openıd Connect bir uygulama tooperform oturum açma için gerekli hello bilgilerin çoğunu içeren bir meta veri belgesi açıklar. Bu hello URL'leri toouse ve hello hizmetin ortak İmzalama anahtarları hello konumunu gibi bilgileri içerir. Merhaba Openıd Connect meta veri belgesi yolda bulunabilir:

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
Basit bir JavaScript nesne gösterimi (JSON) belge Hello meta verilerdir. Aşağıdaki kod parçacığında bir örnek hello bakın. Merhaba parçacığı'nin içeriği tam olarak hello açıklanan [Openıd Connect belirtimi](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Merhaba oturum açma isteği gönder
Web uygulamanızı tooauthenticate hello kullanıcı gerektiğinde Merhaba kullanıcı toohello doğrudan gerekir `/authorize` uç noktası. Bu istek benzer toohello ilk Bacak hello için olan [OAuth 2.0 yetkilendirme kodu akışı](active-directory-protocols-oauth-code.md), birkaç önemli farklılıklar ile:

* Merhaba isteği hello kapsam içermelidir `openid` hello içinde `scope` parametresi.
* Merhaba `response_type` parametre içermelidir `id_token`.
* Merhaba isteği hello içermelidir `nonce` parametresi.

Bu nedenle örnek istek şöyle olabilir:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Parametre |  | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |Merhaba `{tenant}` değeri hello isteği hello yolunda hello uygulamasına oturum kullanılan toocontrol olabilir.  Merhaba izin verilen değerler: Kiracı tanımlayıcıları, örneğin, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` veya `contoso.onmicrosoft.com` veya `common` Kiracı bağımsız belirteçleri |
| client_id |Gerekli |Azure AD ile kaydolurken hello uygulama kimliği atanan tooyour uygulama. Bu hello Azure portalında bulabilirsiniz. Tıklatın **Azure Active Directory**, tıklatın **uygulama kayıtlar**hello uygulamayı seçin ve hello uygulama sayfasında hello uygulama kimliğini bulun. |
| response_type |Gerekli |İçermelidir `id_token` Openıd Connect oturum açma için.  Bu ayrıca diğer response_types gibi içerebilir `code`. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi.  Openıd Connect için bunu hello kapsamını içermelidir `openid`, toohello "oturum" iznini hello izin UI çevirir.  Bu isteği onay isteyen diğer kapsamları ekleyebiliriz. |
| nonce |Gerekli |Merhaba kaynaklanan dahil hello uygulama tarafından üretilen hello isteğinde bulunan bir değer `id_token` bir talep olarak.  Merhaba uygulama daha sonra bu değeri toomitigate belirteç yeniden yürütme saldırılarına doğrulayabilirsiniz.  Merhaba genellikle rastgele, benzersiz dize ya da kullanılan tooidentify hello kaynak hello isteğinin olabilir GUID değeridir. |
| redirect_uri |Önerilen |Burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan, uygulamanızın Hello redirect_uri.  Bu tam olarak bir url kodlanmış olmalıdır dışında hello Portalı'nda kayıtlı hello redirect_uris eşleşmelidir. |
| response_mode |Önerilen |Kullanılan toosend hello elde edilen authorization_code geri tooyour uygulama olmalıdır hello yöntemini belirtir.  Desteklenen değerler `form_post` için *HTTP form post* veya `fragment` için *URL parçası*.  Web uygulamaları için kullanılmasını öneririz `response_mode=form_post` tooensure hello belirteçleri tooyour uygulamanın en güvenli aktarımı. |
| durum |Önerilen |Merhaba belirteci yanıtta döndürülen hello istekte bulunan bir değer.  İstediğiniz herhangi bir içerik dizesi olabilir.  Rastgele oluşturulan benzersiz bir değer tipik olarak kullanılan [siteler arası istek sahteciliğini saldırılarını önleme](http://tools.ietf.org/html/rfc6749#section-10.12).  hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |
| istemi |İsteğe bağlı |Gerekli bir kullanıcı etkileşimi Hello türünü belirtir.  Şu anda, yalnızca geçerli değerler 'oturum açma', 'none' hello ve 'onay'.  `prompt=login`Bu isteğin negating çoklu oturum açma kimlik bilgilerini Hello kullanıcı tooenter zorlar.  `prompt=none`Ters hello - hello kullanıcının tüm etkileşimli istem yoktur ile sunulan değil sağlar.  Merhaba isteği sessizce çoklu oturum açma aracılığıyla tamamlanamazsa, hello uç noktası bir hata döndürür.  `prompt=consent`Merhaba OAuth onay iletişim Hello kullanıcı toogrant izinleri toohello uygulama isteyen hello kullanıcı işaretleri, sonra tetikler. |
| login_hint |İsteğe bağlı |Kullanıcı adlarını önceden biliyorsanız kullanılan toopre dolgu hello kullanıcı adı/e-posta adresi alanı hello kullanıcı oturum açma hello sayfanın olabilir.  Genellikle uygulamaları yeniden kimlik doğrulaması, bir önceki oturum bileşeninden hello kullanıcı adı zaten ayıklanan sırasında bu parametreyi kullanın hello kullanarak `preferred_username` talep. |

Bu noktada, hello kullanıcıdır tooenter kendi kimlik bilgilerini ve tam hello kimlik doğrulaması istedi.

### Örnek yanıt
Merhaba kullanıcı kimliğini doğrulamasından sonra bir örnek yanıt şu şekilde görünebilir:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parametre | Açıklama |
| --- | --- |
| id_token |Merhaba `id_token` istenen bu hello uygulama. Merhaba kullanabilirsiniz `id_token` tooverify kullanıcının kimliğini hello ve hello kullanıcı bir oturumla başlayın. |
| durum |Ayrıca hello belirteci yanıtta döndürülen hello isteği dahil bir değer. Rastgele oluşturulan benzersiz bir değer tipik olarak kullanılan [siteler arası istek sahteciliğini saldırılarını önleme](http://tools.ietf.org/html/rfc6749#section-10.12).  hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |

### Hata yanıtı
Hata yanıtları toohello da gönderilebilir `redirect_uri` hello uygulama bunları uygun şekilde işleyebilmesi için:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

#### Yetkilendirme uç noktası hataları için hata kodları
Merhaba aşağıdaki tabloda açıklanmaktadır hello hello döndürülebilecek çeşitli hata kodları `error` hello hata yanıtı parametresi.

| Hata kodu | Açıklama | İstemci eylemi |
| --- | --- | --- |
| invalid_request |Eksik gerekli parametre gibi protokol hatası. |Düzeltin ve hello isteği yeniden gönderin. Bu geliştirme hata ve genellikle ilk test sırasında yakalandı. |
| unauthorized_client |Merhaba istemci uygulaması olmadığından toorequest bir yetki kodu izin verilir. |Bu durum genellikle, Merhaba istemci uygulaması Azure AD'de kayıtlı değil veya toohello kullanıcının Azure AD kiracısı eklenmez genellikle ortaya çıkar. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |
| ACCESS_DENIED |Kaynak sahibi izin reddedildi |Merhaba istemci uygulaması hello kullanıcı izin sürece devam edemiyor hello kullanıcı bildirebilir. |
| unsupported_response_type |Merhaba yetkilendirme sunucusu hello istekte hello yanıt türünü desteklemiyor. |Düzeltin ve hello isteği yeniden gönderin. Bu geliştirme hata ve genellikle ilk test sırasında yakalandı. |
| server_error |Merhaba sunucu beklenmeyen bir hatayla karşılaştı. |Merhaba isteği yeniden deneyin. Bu hatalar geçici koşulları neden olabilir. Merhaba istemci uygulaması toohello kullanıcı açıklayan yanıt tooa geçici hata ertelendi. |
| temporarily_unavailable |Merhaba geçici olarak meşgul toohandle hello isteği sunucusudur. |Merhaba isteği yeniden deneyin. Merhaba istemci uygulaması toohello kullanıcı açıklayan yanıt tooa geçici koşul ertelendi. |
| invalid_resource |Merhaba hedef kaynak mevcut değil, Azure AD, bulunamıyor veya düzgün yapılandırılmamış olduğundan geçerli değil. |Bu, varsa, hello kaynak hello Kiracı yapılandırılmadı gösterir. Merhaba uygulaması hello uygulama yüklemek ve tooAzure AD eklemek için yönerge hello kullanıcıyla isteyebilir. |

## Merhaba id_token doğrula
Yalnızca alma bir `id_token` yeterli tooauthenticate hello kullanıcı; değil hello imzayı doğrulamak ve hello hello Taleplerde doğrulayın `id_token` uygulamanızın gereksinimleri başına. Hello Azure AD endpoint JSON Web belirteçleri (Jwt'ler) ve ortak anahtar şifrelemesini toosign belirteçleri kullanır ve geçerli olduğunu doğrulayın.

Toovalidate hello seçebilirsiniz `id_token` istemci kodda, ancak toosend hello yaygın bir uygulamadır `id_token` tooa arka uç sunucusuna ve hello doğrulama gerçekleştirin. Merhaba hello imzası doğruladıktan sonra `id_token`, gerekli tooverify olduğunuz birkaç talep vardır.

Ayrıca, ek talep senaryonuza bağlı olarak toovalidate isteyebilir. Bazı ortak doğrulamaları şunları içerir:

* Merhaba kullanıcı/kuruluş sağlama hello uygulaması için kaydolmuş.
* Sağlama hello kullanıcının uygun yetkilendirme/ayrıcalıklara sahip
* Belirli bir kimlik doğrulama gücünü sağlayarak, çok faktörlü kimlik doğrulaması gibi oluştu.

Merhaba doğruladıktan sonra `id_token`, hello kullanıcı bir oturumla başlar ve hello hello talepleri kullanan `id_token` uygulamanızda hello kullanıcı hakkında tooobtain bilgi. Bu bilgiler kullanılabilir ekran kayıtları, yetkilerini, vb. için. Merhaba belirteç türleri ve talepler hakkında daha fazla bilgi için okuma [desteklenen belirteç ve talep türleri](active-directory-token-and-claims.md).

## Oturum kapatma isteği gönder
Toosign hello kullanıcı hello uygulama dışında istediklerinde, uygulamanızın tanımlama bilgilerini yeterli tooclear olduğu veya aksi halde hello kullanıcıyla hello oturumunu sona erdirmek.  Merhaba kullanıcı toohello yönlendirme gerekir `end_session_endpoint` için oturum kapatma.  Toodo nedenle başarısız olursa, geçerli tek bir oturum açma oturumu hello Azure AD uç noktası ile olacağı hello kullanıcı kimlik bilgilerini yeniden girmeden mümkün tooreauthenticate tooyour uygulama olacaktır.

Merhaba kullanıcı toohello yalnızca yönlendirebilirsiniz `end_session_endpoint` hello Openıd Connect meta veri belgesinde listelenen:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| Parametre |  | Açıklama |
| --- | --- | --- |
| post_logout_redirect_uri |Önerilen |Kullanıcı hello hello URL'ye yeniden yönlendirilen tooafter başarılı oturum kapatma olmalıdır.  Dahil edilmezse, hello kullanıcı genel bir ileti gösterilir. |

## Çoklu oturum kapatma
Yönlendirme zaman hello kullanıcı toohello `end_session_endpoint`, Azure AD hello tarayıcı hello kullanıcının oturumunu temizler. Ancak, hello kullanıcı hala Azure AD kimlik doğrulaması için kullanmak tooother uygulamalarda imzalanması. tooenable bu uygulamaları toosign çıkışı kullanıcı aynı anda Merhaba, Azure AD gönderir kayıtlı bir HTTP GET isteği toohello `LogoutUrl` tüm hello uygulamalarının hello kullanıcı şu anda oturum. Uygulamalar gerekir yanıt toothis isteği hello kullanıcı ve döndürme tanımlayan herhangi bir oturumunda temizleyerek bir `200` yanıt.  Uygulamanızda toosupport çoklu oturum kapatma istiyorsanız gibi uygulamalıdır bir `LogoutUrl` uygulamanızın kodu.  Merhaba ayarlayabilirsiniz `LogoutUrl` hello Azure Portalı'ndan:

1. Toohello gidin [Azure Portal](https://portal.azure.com).
2. Active Directory hello sağ üst köşesinde hello sayfa hesabınızda tıklayarak seçin.
3. Merhaba sol taraftaki gezinti panelinden seçin **Azure Active Directory**, ardından **uygulama kayıtlar** ve uygulamanızı seçin.
4. Tıklayın **özellikleri** ve hello bulur **oturum kapatma URL'si** metin kutusu. 

## Belirteç edinme
Birçok web uygulamaları yalnızca oturum hello kullanıcı toonot gerekir, ancak aynı zamanda OAuth kullanarak bu kullanıcı adına bir web hizmetine erişim. Bu senaryo Openıd Connect aynı anda alınırken hatayla kullanıcı kimlik doğrulaması için bir araya getirir bir `authorization_code` kullanılan tooget olabilir `access_tokens` kullanarak hello OAuth yetkilendirme kod akış.

## Erişim belirteci alın
tooacquire erişim belirteçleri, oturum açma toomodify hello isteği üstten gerekir:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

Merhaba isteğine izin kapsamları dahil olmak üzere ve kullanarak `response_type=code+id_token`, hello `authorize` uç nokta sağlar hello kullanıcı hello belirtilen toohello izin verdiği `scope` sorgu parametresi ve uygulamanızı dönüş yetkilendirme kodu bir erişim belirteci tooexchange.

### Başarılı yanıt
Başarılı yanıt kullanarak `response_mode=form_post` gibi görünüyor:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parametre | Açıklama |
| --- | --- |
| id_token |Merhaba `id_token` istenen bu hello uygulama. Merhaba kullanabilirsiniz `id_token` tooverify kullanıcının kimliğini hello ve hello kullanıcı bir oturumla başlayın. |
| Kod |İstenen uygulama hello hello authorization_code. Merhaba uygulama hello yetkilendirme kodu toorequest bir erişim belirteci hello hedef kaynak için kullanabilirsiniz. Authorization_codes kısa süreli ve genellikle yaklaşık 10 dakika sonra süresi dolacak. |
| durum |Bir durum parametresi hello istekte yer alıyorsa hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama hello durum değerleri hello istek ve yanıtta özdeş olduğunu doğrulamanız gerekir. |

### Hata yanıtı
Hata yanıtları toohello da gönderilebilir `redirect_uri` hello uygulama bunları uygun şekilde işleyebilmesi için:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

Merhaba olası hata kodları ve bunların önerilen istemci eylemi açıklaması için bkz: [yetkilendirme uç noktası hataları için hata kodları](#error-codes-for-authorization-endpoint-errors).

Bir yetkilendirme kabulünüzü sonra `code` ve bir `id_token`, hello kullanıcı oturum açabilir ve onların adına erişim belirteci alın.  toosign hello kullanıcı hello doğrulamak gerekir `id_token` tam olarak yukarıda açıklandığı gibi. tooget erişim belirteçleri, hello "Merhaba yetkilendirme kodu toorequest bir erişim belirteci kullan" bölümünde açıklanan başlangıç adımları izleyin bizim [OAuth Protokolü belgeleri](active-directory-protocols-oauth-code.md).
