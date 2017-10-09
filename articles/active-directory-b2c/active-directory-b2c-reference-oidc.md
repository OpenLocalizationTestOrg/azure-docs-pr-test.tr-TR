---
title: "Web Openıd Connect - Azure AD B2C ile oturum açma | Microsoft Docs"
description: "Hello Azure Active Directory uygulaması hello Openıd Connect kimlik doğrulama protokolü kullanarak web uygulamaları oluşturma"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C: Web oturum açma Openıd Connect ile
Openıd Connect tooweb uygulamalarda kullanılan toosecurely oturum kullanıcıların olabilecek OAuth 2.0 üstünde yerleşik bir kimlik doğrulama, protokolüdür. Openıd Connect hello Azure Active Directory B2C (Azure AD B2C) uygulaması kullanarak devredebilir kaydolma, oturum açma ve diğer kimlik yönetimi deneyimleri, web uygulamaları tooAzure Active Directory (Azure AD). Bu kılavuz size nasıl gösterir toodo bir dilden bağımsız şekilde bunu. Açıkladığı nasıl toosend ve bizim açık kaynak kitaplıkları kullanmadan HTTP iletileri alabilirsiniz.

[Openıd Connect](http://openid.net/specs/openid-connect-core-1_0.html) hello OAuth 2.0 genişletir *yetkilendirme* protokolü olarak kullanmak için bir *kimlik doğrulaması* protokolü. Bu, tooperform çoklu oturum açma OAuth kullanılarak sağlar. Merhaba kavramını sunmaktadır bir *kimliği belirteci*, hello istemci tooverify izin veren bir güvenlik belirteci olduğu hello hello kullanıcı kimliğini ve hello kullanıcı hakkında temel profil bilgi edinme.

OAuth 2.0 genişletir çünkü toosecurely elde uygulamalar ayrıca sağlar *erişim belirteçleri*. Tarafından güvenli hale getirilen access_tokens tooaccess kaynakları kullanabilir bir [yetkilendirme sunucusu](active-directory-b2c-reference-protocols.md#the-basics). Bir sunucuda barındırılan ve tarayıcı aracılığıyla erişilen bir web uygulaması oluşturuyorsanız Openıd Connect öneririz. Azure AD B2C kullanarak mobil veya Masaüstü tooadd Kimlik Yönetimi tooyour uygulamaları istiyorsanız, kullanması gereken [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) Openıd Connect yerine.

Azure AD B2C hello standart Openıd Connect Protokolü toodo birden çok basit kimlik doğrulama ve yetkilendirme genişletir. Merhaba tanıtır [İlkesi parametresi](active-directory-b2c-reference-policies.md), sağlayan toouse tooadd kullanıcı deneyimleri Openıd Connect--gibi kaydolma, oturum açma ve profil Yönetimi--tooyour uygulama. Burada, nasıl gösteriyoruz web uygulamalarınızın her birinde karşılaştığında toouse Openıd Connect ve ilkeleri tooimplement. Ayrıca, nasıl tooget erişim belirteçleri erişmek için API web göstereceğiz.

Merhaba örnek HTTP isteklerini hello sonraki bölümde bizim örnek B2C dizini, fabrikamb2c.onmicrosoft.com, yanı sıra bizim örnek uygulama, https://aadb2cplayground.azurewebsites.net ve ilkeleri kullanın. Ücretsiz tootry hello Giden istekleri kendiniz bu değerleri kullanarak veya bunları kendi ile değiştirebilirsiniz.
Nasıl çok öğrenin[kendi B2C Kiracı, uygulama ve ilkeleri alma](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Kimlik doğrulama isteklerini gönderme
Web uygulamanızı tooauthenticate hello kullanıcı gerekir ve bir ilke yürütme zaman hello kullanıcı toohello yönlendirebilirsiniz `/authorize` uç noktası. Bu hello etkileşimli hello akış burada hello kullanıcı, hello ilkesine bağlı olarak eylemde bölümüdür.

Bu istekte hello istemcisi hello izinleri hello hello kullanıcıdan tooacquire gerektiğini belirtir. `scope` hello parametre ve hello İlkesi tooexecute `p` parametresi. Üç örnek bölümlerle (okunabilirlik için satır sonu), aşağıdaki hello içinde her farklı ilke kullanılarak sağlanır. tooget bir fikir her istek işleyişi için bir tarayıcı ile çalışan yapıştırma hello isteği deneyin.

#### <a name="use-a-sign-in-policy"></a>Bir oturum açma ilkesini kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Kayıt İlkesi'ni kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Bir profili Düzenle ilkesini kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [Azure portal](https://portal.azure.com/) tooyour uygulama atanmış. |
| response_type |Gerekli |bir kimliği belirteci Openıd Connect içermelidir hello yanıt türü. Ayrıca web uygulamanızı bir web API'sini çağırmak için belirteçleri ihtiyaç duyuyorsa kullanabileceğiniz `code+id_token`biz burada yaptığınız gibi. |
| redirect_uri |Önerilen |Merhaba `redirect_uri` burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan, uygulamanızın parametresi. Bu tam olarak hello birini eşleşmelidir `redirect_uri` URL kodlanmış olmalıdır ancak bu hello Portalı'nda kayıtlı parametreleri. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi. Tek bir kapsam değeri tooAzure AD istenen iki izinleri gösterir. Merhaba `openid` kapsam kimliği belirteçleri (daha fazla toocome bu hello makalenin sonraki bölümlerinde yer) hello biçiminde hello kullanıcı hakkında hello kullanıcı ve get verilerdeki izni toosign gösterir. Merhaba `offline_access` kapsamı web uygulamaları için isteğe bağlı değil. Uygulamanıza gerekecek gösteren bir *yenileme belirteci* uzun süreli erişim tooresources için. |
| response_mode |Önerilen |kullanılan toosend hello elde edilen yetkilendirme kodu geri tooyour uygulama olmalıdır hello yöntemi. Ya da olabilir `query`, `form_post`, veya `fragment`.  Merhaba `form_post` yanıt modu için en iyi güvenlik önerilir. |
| durum |Önerilen |Ayrıca hello belirteci yanıtta döndürülen hello isteği dahil bir değer. İstediğiniz herhangi bir içerik dizesi olabilir. Rastgele oluşturulan benzersiz bir değer genellikle siteler arası istek sahteciliği saldırılarına önlemek için kullanılır. Başlangıç sayfası üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello ayrıca hello kullanıcı durumunun hello uygulamasında kullanılan tooencode bilgilerini durumudur. |
| nonce |Gerekli |Hello elde edilen kimliği belirteç talep olarak dahil edilecek (Merhaba uygulama tarafından oluşturulan) hello istekte bulunan bir değer. Merhaba uygulama daha sonra bu değeri toomitigate belirteç yeniden yürütme saldırılarına doğrulayabilirsiniz. Merhaba genellikle kullanılan tooidentify hello kaynak hello isteğinin olabilecek rastgele benzersiz bir dize değeridir. |
| P |Gerekli |yürütülecek hello ilkesi. Bu hello B2C kiracınızda oluşturulan bir ilkenin adıdır. Hello ilkesi adı değeri ile başlamalıdır `b2c\_1\_`. İlkeleri ve hello hakkında daha fazla bilgi edinmek [Genişletilebilir ilke çerçevesini](active-directory-b2c-reference-policies.md). |
| istemi |İsteğe bağlı |gerekli bir kullanıcı etkileşimi Hello türü. Merhaba şu anda yalnızca geçerli değer: `login`, hangi kullanıcıların kimlik bilgilerini bu isteğin zorlar hello kullanıcı tooenter. Çoklu oturum açma etkili olmaz. |

Bu noktada, hello kullanıcı toocomplete hello İlkesi'nin iş akışı istedi. Bu, kullanıcı adını ve parolasını girerek hello kullanıcı hello dizin ya da herhangi bir hello İlkesi nasıl tanımlandığına bağlı olarak adım sayısı için kaydolan bir sosyal kimlik bilgilerinizle oturum gerektirebilir.

Merhaba kullanıcı hello İlkesi tamamlandıktan sonra Azure AD hello belirtilen bir yanıt tooyour uygulamaya döndürür `redirect_uri` hello belirtilen hello yöntemi kullanarak parametresi `response_mode` parametresi. Merhaba yanıt olan hello aynı her durumda, yürütülen hello İlkesi bağımsız önceki hello için.

Başarılı yanıt kullanarak `response_mode=fragment` gibi görünür:

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametre | Açıklama |
| --- | --- |
| id_token |İstenen uygulama hello kimliği belirteci hello. Merhaba kullanıcıyla oturumu başlatmak ve hello kimliği belirteci tooverify hello kullanıcının kimliğini kullanın. Kimlik belirteçlerini ve içerikleri hakkında daha fazla ayrıntı hello dahil edilen [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). |
| Kod |Merhaba yetkilendirme kodu istenen bu hello uygulama kullandıysanız `response_type=code+id_token`. Merhaba uygulama için bir hedef kaynak hello yetkilendirme kodu toorequest bir erişim belirteci kullanabilirsiniz. Yetkilendirme kodları çok kısa ömürlüdür. Genellikle, yaklaşık 10 dakika sonra süresi. |
| durum |Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama bu hello doğrulamalısınız `state` hello istek ve yanıt değerler aynı. |

Hata yanıtları toohello da gönderilebilir `redirect_uri` bu hello uygulama bunları uygun şekilde işleyebilmesi için parametre:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametre | Açıklama |
| --- | --- |
| error |Kullanılan tooclassify tür oluşan ve kullanılan tooreact tooerrors olabilir hataları olabilir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| durum |Bu bölümdeki ilk tablo hello Hello tam açıklamaya bakın. Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama bu hello doğrulamalısınız `state` hello istek ve yanıt değerler aynı. |

## <a name="validate-hello-id-token"></a>Merhaba kimliği belirtecini doğrula
Yalnızca bir kimliği belirteci alma yeterli tooauthenticate hello kullanıcı değil. Merhaba kimliği belirtecin imzayı doğrulamak ve uygulamanızın gereksinimleri başına hello belirtecindeki hello talep doğrulamanız gerekir. Azure AD B2C kullanan [JSON Web belirteçleri (Jwt'ler)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) ve ortak anahtar şifrelemesi toosign belirteçleri ve geçerli olduğunu doğrulayın.

Jwt'ler, tercih dilinizi bağlı olarak doğrulamak için kullanılabilen birçok açık kaynak kitaplıkları vardır. Kendi doğrulama mantığı uygulamak yerine bu seçenekleri keşfetme öneririz. Buraya Hello bilgileri nasıl tooproperly kullandığını bu kitaplıkları anlamak yararlı olacaktır.

Azure AD B2C, bir uygulama toofetch hakkında bilgi Azure AD B2C çalışma zamanında sağlayan bir Openıd Connect meta veri uç noktası, sahiptir. Bu bilgiler, uç noktaları, belirteç içerikleri ve belirteç imzalama anahtarları içerir. B2C kiracınızda her ilke için bir JSON meta veri belgesi yoktur. Örneğin, hello meta veri belgesi hello için `b2c_1_sign_in` ilkesinde `fabrikamb2c.onmicrosoft.com` bulunur:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Bu yapılandırma belgenin hello özellikleri biri `jwks_uri`, değeri aynı ilke olacaktır hello için:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

hangi ilke kullanıldı toodetermine kimliği belirteç imzalama (ve burada toofetch hello meta veriler), iki seçeneğiniz vardır. Hello ilkesi adı hello ilk olarak dahil `acr` hello kimliği belirteçte talep. Merhaba nasıl tooparse hello kimliği belirtecinden talepleri hakkında daha fazla bilgi için bkz [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). Diğer seçeneğiniz tooencode hello hello hello değeri ilkedir `state` sorun hello istek ve hangi ilke kullanıldı toodetermine kod çözme parametresi. Her iki yöntem geçerli değil.

Merhaba meta veri belgesi hello Openıd Connect meta veri uç noktasından edindiğiniz sonra (Bu uç noktada bulunur) hello RSA 256 ortak anahtarlarını kullanabilirsiniz hello kimliği belirtecinin toovalidate hello imzası. Verilen herhangi bir noktada Bu uç noktada zamanında listelenen birden çok anahtar olabilir, her tarafından tanımlanan bir `kid` talep. Merhaba hello kimliği belirteci üstbilgisinin de içeren bir `kid` talep, kullanılan toosign hello kimliği belirteci bu anahtarların olduğu gösterir. Merhaba daha fazla bilgi için bkz [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md) (Merhaba bölüm [belirteçleri doğrulama](active-directory-b2c-reference-tokens.md#token-validation), özellikle).
<!--TODO: Improve hello information on this-->

Merhaba kimliği belirtecinin imzası hello doğruladıktan sonra birkaç talep tooverify ihtiyacınız vardır. Örneğin:

* Merhaba doğrulamalıdır `nonce` tooprevent belirteç yeniden yürütme saldırılarını talep. Oturum açma hello istekte belirtilen değeri olmalıdır.
* Merhaba doğrulamalıdır `aud` kimliği belirteci hello tooensure, uygulamanız için yayımlandığında talep. Değeri, uygulamanızın hello uygulama kimliği olmalıdır.
* Merhaba doğrulamalıdır `iat` ve `exp` talep kimliği belirteci hello tooensure süresi.

Gerçekleştirmeniz gereken birkaç daha fazla doğrulama vardır. Bunlar hello ayrıntılı açıklanmıştır [Openıd Connect çekirdek Spec](http://openid.net/specs/openid-connect-core-1_0.html).  Senaryonuza bağlı olarak toovalidate ek talepleri de isteyebilirsiniz. Bazı ortak doğrulamaları şunları içerir:

* Kullanıcı/kuruluş hello sağlama hello uygulaması için kaydolmuş.
* Merhaba kullanıcının uygun yetkilendirme/ayrıcalıklara sahip olma.
* Belirli bir kimlik doğrulama gücünü, Azure multi-Factor Authentication gibi oluştuğunu sağlama.

Merhaba hello talep kimliği belirteci hakkında daha fazla bilgi için bkz: [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md).

Merhaba kimliği belirteci doğrulandıktan sonra bir oturum hello kullanıcıyla başlayabilirsiniz. Uygulamanızda hello kullanıcı hakkında hello kimliği belirteci tooobtain bilgi hello talep kullanabilirsiniz. Bu bilgiler kullanımları görüntüleme, kayıtları ve yetkilendirme içerir.

## <a name="get-a-token"></a>Belirteç alın
Web uygulaması tooonly gerekiyorsa ilkeleri yürütmek, atlayabilirsiniz hello sonraki birkaç bölümler. Bu bölümler, kimliği doğrulanmış toomake çağrıları tooa web API gerekir ve Azure AD B2C tarafından korunmuş geçerli yalnızca tooweb uygulamalardır.

Aldığınız hello yetkilendirme kodu kullanın (kullanarak `response_type=code+id_token`) için bir belirteç toohello istenen kaynak göndererek bir `POST` toohello isteği `/token` uç noktası. Şu anda hello için bir belirteç isteyebileceği yalnızca uygulamanın kendi arka uç web API kaynaktır. belirteç tooyourself isteyen hello uygulamanızın istemci kimliği, hello kapsamı olarak toouse kuraldır:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| P |Gerekli |Merhaba, kullanılan tooacquire hello yetkilendirme ilkesi kodu. Bu isteği başka bir ilke kullanamazsınız. Bu parametre toohello sorgu dizesi, değil toohello eklediğiniz Not `POST` gövdesi. |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [Azure portal](https://portal.azure.com/) tooyour uygulama atanmış. |
| grant_type |Gerekli |Merhaba olmalıdır grant türünü `authorization_code` hello yetkilendirme kodu akışı. |
| Kapsam |Önerilen |Kapsamları boşlukla ayrılmış listesi. Tek bir kapsam değeri tooAzure AD istenen iki izinleri gösterir. Merhaba `openid` kapsamını izni toosign id_token parametreleri hello biçiminde hello kullanıcı hakkında hello kullanıcı ve get verilerdeki belirtir. Hangi hello tarafından temsil edilen kullanılan tooget belirteçleri tooyour uygulamanın kendi arka uç web API'si, olabilir hello istemcisi olarak aynı uygulama kimliği. Merhaba `offline_access` kapsamını belirtir, uygulamanız için uzun süreli erişim tooresources bir yenileme belirteci gerekir. |
| Kod |Gerekli |Merhaba akışının hello ilk leg aldığınız hello yetkilendirme kodu. |
| redirect_uri |Gerekli |Merhaba `redirect_uri` hello yetkilendirme kodu aldığınız hello uygulama parametresi. |
| client_secret |Gerekli |hello oluşturulan hello uygulama gizli anahtarı [Azure portal](https://portal.azure.com/). Bu uygulama gizli anahtarı bir önemli güvenlik yapıdır. Onu güvenli bir şekilde sunucunuzda depolamanız gerekir. Ayrıca bu gizli düzenli aralıklarla döndürme. |

Başarılı bir token yanıt şuna benzer:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parametre | Açıklama |
| --- | --- |
| not_before |hangi hello belirteci geçerli dönem zamanında kabul hello süre. |
| token_type |Merhaba belirteç türü değeri. yalnızca Azure AD destekler türü hello `Bearer`. |
| access_token |Merhaba, istenen JWT belirteci imzalayan. |
| Kapsam |Merhaba kapsamlar için hangi hello belirtecin geçerli olduğu. Bu, daha sonra kullanmak için belirteç önbelleğe almak için kullanılabilir. |
| expires_in |erişim belirteci hello süre Hello uzunluğu (saniye olarak) geçerli değil. |
| refresh_token |Bir OAuth 2.0 yenileme belirteci. Merhaba geçerli belirteç süresi dolduktan sonra bu belirteci tooacquire ek belirteçler hello uygulamasını kullanabilir. Yenileme belirteçleri uzun süreli ve uzun süre için kullanılan tooretain erişim tooresources olabilir. Daha fazla ayrıntı için toohello başvurun [B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). Merhaba kapsam kullanılan gerekir Not `offline_access` hello yetkilendirme ve belirteç sipariş tooreceive bir yenileme belirteci ister. |

Hata yanıtları gibi görünür:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametre | Açıklama |
| --- | --- |
| error |Kullanılan tooclassify tür oluşan ve kullanılan tooreact tooerrors olabilir hataları olabilir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

## <a name="use-hello-token"></a>Merhaba belirteci kullanın
Bir erişim belirteci başarıyla edindiğiniz, hello belirteç isteklerini tooyour arka uç web API'leri hello dahil ederek kullanabileceğiniz `Authorization` üstbilgisi:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Merhaba belirtecini yenileme
Kimlik belirteçlerini ömürlüdür. Mümkün tooaccess kaynakları olan toocontinue parolalarının süresi dolduktan sonra bunları yenilemeniz gerekir. Başka bir göndererek yapabilirsiniz `POST` toohello isteği `/token` uç noktası. Bu süre, hello sağlamak `refresh_token` parametre hello yerine `code` parametre:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| Parametre | Gerekli | Açıklama |
| --- | --- | --- |
| P |Gerekli |kullanılan tooacquire hello özgün yenileme belirteci olan hello ilkesi. Bu isteği başka bir ilke kullanamazsınız. Bu parametre toohello sorgu dizesi, toohello POST gövde eklediğiniz unutmayın. |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [Azure portal](https://portal.azure.com/) tooyour uygulama atanmış. |
| grant_type |Gerekli |Bu leg hello yetkilendirme kodu akışı için bir yenileme belirteci olmalıdır grant Hello türü. |
| Kapsam |Önerilen |Kapsamları boşlukla ayrılmış listesi. Tek bir kapsam değeri tooAzure AD istenen iki izinleri gösterir. Merhaba `openid` kapsam kimliği belirteçleri hello biçiminde hello kullanıcı hakkında hello kullanıcı ve get verilerdeki izni toosign gösterir. Hangi hello tarafından temsil edilen kullanılan tooget belirteçleri tooyour uygulamanın kendi arka uç web API'si, olabilir hello istemcisi olarak aynı uygulama kimliği. Merhaba `offline_access` kapsamını belirtir, uygulamanız için uzun süreli erişim tooresources bir yenileme belirteci gerekir. |
| redirect_uri |Önerilen |Merhaba `redirect_uri` hello yetkilendirme kodu aldığınız hello uygulama parametresi. |
| refresh_token |Gerekli |Merhaba akışının hello ikinci leg edindiğiniz hello özgün yenileme belirteci. Merhaba kapsam kullanılan gerekir Not `offline_access` hello yetkilendirme ve belirteç sipariş tooreceive bir yenileme belirteci ister. |
| client_secret |Gerekli |hello oluşturulan hello uygulama gizli anahtarı [Azure portal](https://portal.azure.com/). Bu uygulama gizli anahtarı bir önemli güvenlik yapıdır. Onu güvenli bir şekilde sunucunuzda depolamanız gerekir. Ayrıca bu gizli düzenli aralıklarla döndürme. |

Başarılı bir token yanıt şuna benzer:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parametre | Açıklama |
| --- | --- |
| not_before |hangi hello belirteci geçerli dönem zamanında kabul hello süre. |
| token_type |Merhaba belirteç türü değeri. yalnızca Azure AD destekler türü hello `Bearer`. |
| access_token |Merhaba, istenen JWT belirteci imzalayan. |
| Kapsam |Daha sonra kullanmak için belirteç önbelleğe almak için kullanılabilecek belirteci hello hello kapsam için geçerli değil. |
| expires_in |erişim belirteci hello süre Hello uzunluğu (saniye olarak) geçerli değil. |
| refresh_token |Bir OAuth 2.0 yenileme belirteci. Merhaba geçerli belirteç süresi dolduktan sonra bu belirteci tooacquire ek belirteçler hello uygulamasını kullanabilir.  Yenileme belirteçleri uzun süreli ve uzun süre için kullanılan tooretain erişim tooresources olabilir. Daha fazla ayrıntı için toohello başvuran [B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). |

Hata yanıtları gibi görünür:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametre | Açıklama |
| --- | --- |
| error |Kullanılan tooclassify tür oluşan ve kullanılan tooreact tooerrors olabilir hataları olabilir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

## <a name="send-a-sign-out-request"></a>Oturum kapatma isteği gönder
Toosign hello kullanıcı hello uygulama dışında istediğinizde, uygulamanızın tanımlama bilgilerini yeterli tooclear olduğu veya aksi halde hello kullanıcıyla hello oturumunu sona erdirmek. Ayrıca hello kullanıcı tooAzure AD toosign giden yönlendirmesi gerekir. Toodo nedenle başarısız olursa, hello kullanıcı kimlik bilgilerini yeniden girmeden mümkün tooreauthenticate tooyour uygulama olabilir. Bu durum, geçerli tek bir oturum açma oturumu Azure AD ile gerekir çünkü.

Merhaba kullanıcı toohello yalnızca yönlendirebilirsiniz `end_session` hello Openıd Connect meta veri belgesinde listelenen endpoint önceki hello "Merhaba kimliği belirtecini doğrula" bölümünde açıklanan:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| P |Gerekli |hello İlkesi toouse toosign hello kullanıcı uygulamanızı dışında istiyor. |
| post_logout_redirect_uri |Önerilen |Merhaba hello kullanıcının yeniden yönlendirilen tooafter başarılı olmalıdır oturum kapatma. Dahil edilmezse, Azure AD B2C hello kullanıcı genel bir ileti gösterir. |

> [!NOTE]
> Merhaba kullanıcı toohello yönlendirerek rağmen `end_session` uç nokta bazı Azure AD B2C ile Merhaba kullanıcının tek oturum açma durumu Temizle, sosyal kimlik sağlayıcıyı (IDP) oturumuna dışında hello kullanıcı oturum yok. Merhaba kullanıcı seçerse bir sonraki oturum açma sırasında aynı IDP Merhaba, bunlar, kullanıcıların kimlik bilgilerini girmeden kimliğinin yeniden doğrulanması. Bir kullanıcı toosign B2C uygulamanızı dışında isterse, mutlaka Facebook hesaplarında dışında toosign istedikleri anlamına gelmez. Ancak, yerel hesaplar hello durumda hello kullanıcının oturumunu düzgün sonlandırılır.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>B2C kiracısına kullanın
Tootry bu istekleri kendiniz istiyorsanız ilk üç bu adımları uygulayın ve ardından daha önce kendi açıklanan hello örnek değerleri değiştirin:

1. [B2C kiracısı oluşturma](active-directory-b2c-get-started.md)ve hello isteklerinde kiracınızın hello adını kullanın.
2. [Uygulama oluşturma](active-directory-b2c-app-registration.md) tooobtain bir uygulama kimliği Bir web uygulaması/web API uygulamanızı içerir. İsteğe bağlı olarak, bir uygulama gizli anahtarı oluşturun.
3. [İlkelerinizi oluşturma](active-directory-b2c-reference-policies.md) tooobtain ilke adları.

