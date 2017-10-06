---
title: "Azure Active Directory B2C: Belirteç başvurusu | Microsoft Docs"
description: "Azure Active Directory B2C'de yayınlanan belirteçleri Hello türleri"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C: Belirteç başvurusu
Azure Active Directory B2C (Azure AD B2C) her işlediği gibi çeşitli güvenlik belirteçleri yayar [kimlik doğrulaması akışı](active-directory-b2c-apps.md). Bu belgede hello biçimi, güvenlik özellikleri ve her tür bir belirteç içeriği açıklanmaktadır.

## <a name="types-of-tokens"></a>Belirteç türleri
Azure AD B2C destekleyen hello [OAuth 2.0 yetkilendirme protokolünü](active-directory-b2c-reference-protocols.md), erişim belirteçleri ve yenileme belirteçleri hangi her ikisini de kullanır. Kimlik doğrulama ve oturum açma aracılığıyla da destekler [Openıd Connect](active-directory-b2c-reference-protocols.md), bir üçüncü Belirtecin türü sunar: hello kimliği belirteci. Her Bu belirteçler, taşıyıcı belirteç olarak temsil edilir.

Bir basit güvenlik belirteci verir "bearer" erişim tooa hello korumalı kaynak bir taşıyıcı belirtecidir. Merhaba taşıyıcı hello belirteci sunabilir herhangi bir tarafa ' dir. Bir taşıyıcı belirteci almak için önce azure AD önce bir taraf kimlik doğrulaması gerekir. Ancak adımları toosecure hello belirteçte iletim ve depolama katılmaz hello gerekli olursa, kullanılabilir engelledik ve istenmeyen bir şirket tarafından kullanılan. Bazı güvenlik belirteçleri kullanarak gelen yetkisiz tarafların engellemek için yerleşik bir mekanizma sahip, ancak taşıyıcı belirteçlerini bu düzenek sahip değil. Bunlar Aktarım Katmanı Güvenliği (HTTPS) gibi güvenli bir kanal taşınan gerekir.

Bir taşıyıcı belirteci dışında güvenli bir kanal iletilirse, kötü amaçlı bir taraf man-in--middle saldırı tooacquire hello belirteci kullanın ve toogain yetkisiz erişim korumalı tooa kaynak kullanın. Merhaba depolanan ya da daha sonra kullanmak üzere önbelleğe taşıyıcı belirteçlerini aynı güvenlik ilkeleri uygulayın. Her zaman uygulamanızı aktarır ve güvenli bir şekilde taşıyıcı belirteçleri depolar emin olun.

Taşıyıcı belirteçlerini üzerinde ek güvenlik konuları için bkz: [RFC 6750 bölüm 5](http://tools.ietf.org/html/rfc6750).

Azure AD B2C sorunları hello belirteçleri çoğunu JSON web belirteçleri (Jwt'ler) uygulanır. JWT, iki taraf arasında bilgi aktarma compact, URL için güvenli bir yoludur. Jwt'ler talepler olarak bilinen bilgiler içerir. Merhaba taşıyıcı hakkındaki bilgilerin onaylar ve hello konu hello belirtecinin bunlar. Jwt'ler Hello Taleplerde kodlanmış ve aktarım için seri hale getirilmiş JSON nesneleridir. Hello Azure AD B2C tarafından verilen Jwt'ler imzalanmış ancak şifreli olduğundan, bir JWT toodebug Merhaba içeriğine kolayca inceleyebilirsiniz onu. Birkaç araç bulunmaktadır, yapabilir dahil olmak üzere bu [calebb.net](http://calebb.net). Jwt'ler hakkında daha fazla bilgi için çok başvuran[JWT belirtimleri](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Kimliği belirteçleri
Bir kimliği belirteci uygulamanızı hello Azure AD B2C ' aldığı güvenlik belirteci biçimidir `authorize` ve `token` uç noktaları. Kimlik belirteçlerini olarak temsil [Jwt'ler](#types-of-tokens), uygulamanızda tooidentify kullanıcılar kullanabileceğiniz talepleri içerir. Ne zaman kimlik belirteçlerini edinilen hello `authorize` uç noktası, sık kullanılan toosign kullanıcılar tooweb uygulamalarında oldukları. Ne zaman kimlik belirteçlerini edinilen hello `token` uç noktası, bunlar gönderilebilir HTTP isteklerinde hello iki bileşenleri arasındaki iletişim sırasında aynı uygulama veya hizmet. Uygun gördüğünüz şekilde hello talep kimliği belirteçte kullanabilirsiniz. Yaygın olarak kullanılan toodisplay hesap bilgileri veya toomake erişim denetimi kararlarını bir uygulamada oldukları.  

Kimlik belirteçlerini imzalanmış, ancak şu anda şifrelenmez. Uygulamanızı veya API kimliği belirteci aldığında, gerekir [hello imzayı doğrulamak](#token-validation) belirteci hello tooprove gerçek. Ayrıca, uygulama veya API birkaç Taleplerde hello belirteci tooprove geçerli olduğunu doğrulamanız gerekir. Merhaba senaryonun gereksinimlerine bağlı olarak, bir uygulama tarafından doğrulanmış hello talep farklılık gösterebilir, ancak uygulamanızı bazı gerçekleştirmelisiniz [ortak talep doğrulamaları](#token-validation) her senaryoda.

#### <a name="sample-id-token"></a>Örnek kimliği belirteci
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>Erişim belirteçleri
Bir erişim belirteci Ayrıca uygulamanızı hello Azure AD B2C ' aldığı güvenlik belirteci biçimidir `authorize` ve `token` uç noktaları. Erişim belirteçleri ayrıca olarak temsil [Jwt'ler](#types-of-tokens), ve izinleri tooyour API'leri verilen tooidentify hello kullanabileceğiniz talepleri içerir. Erişim belirteçleri imzalanmış, ancak şu anda şifrelenmez. Erişim belirteçleri kullanılan tooprovide erişim tooAPIs ve kaynak sunucuları olmalıdır. Hakkında daha fazla çok bilgi[erişim belirteçleri kullanmak](active-directory-b2c-access-tokens.md). 

API'nizi bir erişim belirteci aldığında, gerekir [hello imzayı doğrulamak](#token-validation) belirteci hello tooprove gerçek. API'nizi birkaç Taleplerde hello belirteci tooprove geçerli olduğunu da doğrulamanız gerekir. Merhaba senaryonun gereksinimlerine bağlı olarak, bir uygulama tarafından doğrulanmış hello talep farklılık gösterebilir, ancak uygulamanızı bazı gerçekleştirmelisiniz [ortak talep doğrulamaları](#token-validation) her senaryoda.

### <a name="claims-in-id-and-access-tokens"></a>Kimlik ve erişim belirteçleri talepleri
Azure AD B2C kullandığınızda, belirteçlerinizi Merhaba içeriğine hassas denetime sahip olursunuz. Yapılandırabileceğiniz [ilkeleri](active-directory-b2c-reference-policies.md) toosend belirli ayarlar, kullanıcı verilerinin taleplerdeki kendi işlemleri için uygulamanızı gerektirir. Bu talep hello kullanıcının gibi standart özellikler içerebilir `displayName` ve `emailAddress`. Ayrıca içerebilir [özel kullanıcı öznitelikleri](active-directory-b2c-reference-custom-attr.md) , B2C dizininizde tanımlayabilirsiniz. Her kimlik ve erişim aldığınız belirteç talep güvenlikle ilgili belirli bir kümesini içerir. Uygulamalarınızı toosecurely kullanıcılar ve istekleri kimlik doğrulaması bu talepler kullanabilirsiniz.

Merhaba talep kimliği belirteçlerinde belirli bir sırada döndürülmez unutmayın. Ayrıca, yeni talep kimliği belirteçleri herhangi bir zamanda tanıtılabilir. Yeni Talep sunulduğu şekilde uygulamanızı parçalara değil. İşte hello talep tooexist Azure AD B2C tarafından yayınlanan kimliği ve erişim belirteçleri beklenen. Herhangi bir ek talep ilkeleri tarafından belirlenir. Uygulama için içine yapıştırarak hello örnek kimliği belirtecini hello Taleplerde inceleniyor deneyin [calebb.net](http://calebb.net). Daha ayrıntılı bilgi hello bulunabilir [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html).

| Ad | İste | Örnek değer | Açıklama |
| --- | --- | --- | --- |
| Hedef kitle |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Bir izleyici talep hello hedeflenen alıcı hello belirtecinin tanımlar. Azure AD B2C için hello İzleyici atanan tooyour uygulama hello uygulama kayıt Portalı'nda, uygulamanızın uygulama kimliği, gibidir. Uygulamanız bu değeri doğrulamak ve onu eşleşmiyorsa hello belirteci reddetme gerekir. |
| Veren |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |Bu talep oluşturur ve hello belirteç döndüren hello güvenlik belirteci hizmeti (STS) tanımlar. Ayrıca, hangi hello kullanıcı kimlik doğrulamasının yapıldığı hello Azure AD dizini tanımlar. Uygulamanızı hello verenin talep belirteci hello tooensure hello Azure Active Directory v2.0 uç noktasından gelen doğrulamalıdır. |
| çıkışı |`iat` |`1438535543` |Bu talep sırasında hangi hello belirteci, dönem saatle gösterilir verilmiş hello saattir. |
| süre sonu |`exp` |`1438539443` |Merhaba sona erme saati talep sırasında hangi hello belirteç olur geçersiz, dönem zaman gösterilen hello saattir. Uygulamanızı hello belirteç ömrü bu talep tooverify hello geçerliliğini kullanmanız gerekir. |
| önce değil |`nbf` |`1438535543` |Bu talep sırasında hangi hello belirteç olur geçerli, dönem zaman gösterilen hello saattir. Bu olduğundan genellikle hello aynı hello zaman hello belirteci verildiğinde. Uygulamanızı hello belirteç ömrü bu talep tooverify hello geçerliliğini kullanmanız gerekir. |
| Sürüm |`ver` |`1.0` |Bu hello hello kimliği belirteci, Azure AD tarafından tanımlandığı şekilde sürümüdür. |
| kod karma |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Yalnızca hello belirteci ile birlikte bir OAuth 2.0 yetkilendirme kodu verildiğinde bir kod karma bir kimlik belirtecinde dahil edilir. Kod karma bir kimlik doğrulama kodu kullanılan toovalidate hello özgünlüğünü olabilir. Konusunda daha fazla ayrıntı için tooperform bu doğrulama hello bkz [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html).  |
| erişim belirteci karma |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Yalnızca hello belirteci ile birlikte bir OAuth 2.0 erişim belirteci verildiğinde bir erişim belirteci karma bir kimlik belirtecinde dahil edilir. Bir erişim belirteci karma bir erişim belirteci kullanılan toovalidate hello özgünlüğünü olabilir. Konusunda daha fazla ayrıntı için tooperform bu doğrulama hello bkz [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html)  |
| nonce |`nonce` |`12345` |Nonce bir strateji toomitigate belirteç yeniden yürütme saldırılarını kullanılır. Uygulamanızı bir nonce bir yetkilendirme isteği hello kullanarak belirtebilirsiniz `nonce` sorgu parametresi. Merhaba istekte sağladığınız hello değeri yayılan hello değiştirilmemiş `nonce` yalnızca bir kimliği belirtecini talep. Bu, uygulama tooverify hello değeri hello uygulamanın oturumunu belirli bir kimliği belirteciyle ilişkilendirir hello isteğinde belirtilen hello değeri karşı sağlar. Uygulamanızı hello kimliği belirteci doğrulama işlemi sırasında bu doğrulama gerçekleştirmeniz gerekir. |
| Konu |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Hangi hello hakkında hello kullanıcı, bir uygulamanın gibi bilgileri belirteci onaylar hello asıl budur. Bu değer sabittir ve yeniden atandığında yeniden ya da silinemez. Merhaba belirteci kullanılan tooaccess bir kaynak olduğunda gibi bu kullanılan tooperform yetkilendirme denetimleri güvenli bir biçimde olabilir. Varsayılan olarak, hello konu talep hello dizininde hello kullanıcı hello nesne kimliği ile doldurulur. toolearn daha, fazla [Azure Active Directory B2C: belirteci, oturum ve tek oturum açma yapılandırması](active-directory-b2c-token-session-sso.md). |
| Kimlik doğrulama bağlamı sınıf başvurusu |`acr` |Uygulanamaz |Şu anda kullanılmayan, hariç eski ilkeleri hello durumda. toolearn daha, fazla [Azure Active Directory B2C: belirteci, oturum ve tek oturum açma yapılandırması](active-directory-b2c-token-session-sso.md). |
| Güven Framework İlkesi |`tfp` |`b2c_1_sign_in` |Bu hello kullanılan tooacquire hello kimliği belirteci olan hello İlkesi adıdır. |
| Kimlik doğrulama süresi |`auth_time` |`1438535543` |Bu talep bir kullanıcı son girilen kimlik bilgileri, dönem zamanında temsil hello saattir. |

### <a name="refresh-tokens"></a>Yenileme belirteçlerini
Yenileme belirteçleri olan uygulamanızı tooacquire yeni kimliği belirteçleri kullanın ve erişim belirteçleri bir OAuth 2.0 akışı güvenlik belirteçleri. Uygulamanız ile uzun vadeli erişim tooresources kullanıcıların adına kullanıcılarla ile etkileşimi gerektirmeden sağlarlar.

bir yenileme belirteci bir belirteç yanıt tooreceive, uygulamanızı istemeniz gerekir hello `offline_acesss` kapsam. Merhaba hakkında daha fazla toolearn `offline_access` kapsam, toohello başvuran [Azure AD B2C Protokolü başvurusu](active-directory-b2c-reference-protocols.md).

Yenileme belirteçlerini olan ve her zaman olacak, tamamen opak tooyour uygulama. Bunlar Azure AD tarafından verilen ve Denetlenmekte ve yalnızca Azure AD tarafından yorumlanır. Uzun süreli, ancak bir yenileme belirteci belirli bir döneme ait en son hello beklentisi ile uygulamanızı yazılmamalıysa. Çeşitli nedenlerle için herhangi bir anda yenileme belirteçleri geçersiz olabilir. bir yenileme belirteci geçerliyse, uygulama tooknow tooattempt tooredeem yoldur yalnızca Merhaba, belirteç isteği tooAzure AD yaparak.

Bir yenileme belirteci için yeni bir belirteç almak zaman (ve uygulamanızı hello verilirse `offline_access` kapsam), hello belirteci yanıt olarak yeni bir yenileme belirteci alırsınız. Yeni verilen hello yenileme belirteci kaydetmeniz gerekir. Daha önce hello istekte kullanılan hello yenileme belirteci değiştirmeniz gerekir. Bu, yenileme belirteçleri mümkün olduğunca uzun bir süre geçerli kalacağını garanti yardımcı olur.

## <a name="token-validation"></a>Belirteç doğrulama
toovalidate bir belirteci, uygulamanızı hello imza ve hello belirteci taleplerini kontrol etmeniz gerekir.

Birçok açık kaynak kitaplıkları Jwt'ler, tercih ettiğiniz dili bağlı olarak doğrulamak için kullanılabilir. Bu seçenek keşfetmek yerine kendi doğrulama mantığını uygulamak öneririz. Bu kılavuzdaki Hello bilgilerini tooproperly bu kitaplıklarını nasıl kullanacağınızı öğrenin yardımcı olabilir.

### <a name="validate-hello-signature"></a>Merhaba imza doğrulama
JWT'nin hello tarafından ayrılmış üç parçaları içeren `.` karakter. Merhaba ilk kesimi ise hello *üstbilgi*, hello ikinci hello olan *gövde*, ve hello üçüncü hello *imza*. Böylece, uygulamanız tarafından güvenilen hello imza segment kullanılan toovalidate hello hello belirteci özgünlüğünü olabilir.

Azure AD B2C belirteç RSA 256 gibi endüstri standardı asimetrik şifreleme algoritmaları kullanılarak imzalanmıştır. Merhaba belirteci Hello üstbilgisi hello anahtarı hakkında bilgi içerir ve toosign hello belirteç şifreleme yöntemi kullanılır:

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

Merhaba `alg` talep kullanılan toosign hello belirteci olan hello algoritmasını belirtir. Merhaba `kid` talep kullanılan toosign hello belirteci olan hello belirli ortak anahtarı gösterir.

Belirli bir zamanda, Azure AD belirli bir genel-özel anahtar çiftleri kümesini herhangi birini kullanarak bir belirteç oturum açabilirsiniz. Uygulamanız bu anahtarı otomatik olarak değiştirir toohandle yazılması gereken şekilde azure AD hello olası anahtarlar kümesi, düzenli aralıklarla döndürür. Azure AD tarafından kullanılan güncelleştirmeleri toohello ortak anahtarları için makul sıklığı toocheck her 24 saattir.

Azure AD B2C Openıd Connect meta veri son nokta vardır. Bu uygulamalar çalışma zamanında Azure AD B2C hakkında toofetch bilgi sağlar. Bu bilgiler, uç noktaları, belirteç içerikleri ve belirteç imzalama anahtarları içerir. Her ilke için bir JSON meta veri belgesi, B2C dizini içerir. Örneğin, hello meta veri belgesi hello için `b2c_1_sign_in` ilkesinde `fabrikamb2c.onmicrosoft.com` bulunur:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`olan hello B2C dizini kullanılan tooauthenticate hello kullanıcı ve `b2c_1_sign_in` olduğu hello İlkesi tooacquire hello belirteci kullanılır. hangi ilke kullanılan toosign bir belirteç olan (ve burada toogo toofetch hello meta veriler), toodetermine iki seçeneğiniz vardır. Hello ilkesi adı hello ilk olarak dahil `acr` hello belirteçte talep. Merhaba JWT hello gövdesi base-64 kod çözme hello gövde tarafından dışında talep ayrıştırabilir ve hello seri durumdan JSON dize sonucu. Merhaba `acr` talep kullanılan tooissue hello belirteci olan hello İlkesi hello adı olacaktır.  Diğer seçeneğiniz tooencode hello hello hello değeri ilkedir `state` sorun hello istek ve hangi ilke kullanıldı toodetermine kod çözme parametresi. Her iki yöntem geçerli değil.

Merhaba meta veri belgesi birkaç yararlı bilgi parçalarını içeren bir JSON nesnesidir. Bunlar hello uç noktaları gerekli tooperform Openıd Connect kimlik doğrulama hello konumunu içerir. Ayrıca içerirler `jwks_uri`, kullanılan toosign belirteçleri ortak anahtarları hello kümesi hello konumunu sağlar. Bu konum burada sağlanan, ancak bunu en iyi toofetch hello konumu dinamik olarak hello meta veri belgesi kullanarak ve çıkışı ayrıştırma `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

Bu URL'de bulunan hello JSON belgesi tüm hello belirli bir anda kullanımda ortak anahtar bilgileri içerir. Uygulamanızı hello kullanabilirsiniz `kid` anahtarında hello JWT üstbilgi tooselect hello ortak kullanılan toosign hello JSON belgesinde belirli bir belirteç talep. Merhaba doğru ortak anahtar ve hello belirtilen algoritma kullanarak bunu imza doğrulaması daha sonra gerçekleştirebilirsiniz.

Bu belgenin dış hello kapsamı tooperform imza doğrulaması nasıl olduğunu açıklaması. Birçok açık kaynak kitaplıkları kullanılabilir toohelp, bu, ihtiyacınız olan.

### <a name="validate-hello-claims"></a>Merhaba talep doğrula
Uygulamanızı veya API kimliği belirteci aldığında, bunu hello talep karşı bazı denetimleri hello kimliği belirteçte gerçekleştirmelisiniz. Bunlar arasında ancak bunlarla sınırlı değildir:

* Merhaba **İzleyici** talep: Bu hello kimliği belirtecini edildi tooyour uygulama verilen hedeflenen toobe doğrular.
* Merhaba **önce değil** ve **süre sonu** talep: Bunlar hello kimliği belirtecini süresi sona doğrulayın.
* Merhaba **veren** talep: Bu hello belirtecini Azure AD tarafından tooyour uygulama yayımlandığında doğrular.
* Merhaba **nonce**: belirteç yeniden yürütme saldırı azaltma için bir strateji budur.

Uygulamanızı gerçekleştirmesi gerektiğini doğrulamaları tam bir listesi için toohello bakın [Openıd Connect belirtimi](https://openid.net). Bu talep için hello beklenen değerler ayrıntılarını hello önceki dahil [belirteci bölüm](#types-of-tokens).  

## <a name="token-lifetimes"></a>Belirteç yaşam süresi
belirteç yaşam süreleri aşağıdaki hello olan toofurther bilginiz sağlanan. Geliştirme ve hata ayıklama uygulamaları bunlar yardımcı olabilir. Uygulamalarınızı olmamalıdır Not tooexpect bu yaşam süreleri tooremain sabiti hiçbirini yazılır. Bunlar olabilir ve değiştirir. Merhaba hakkında daha fazla bilgiyi [belirteci yaşam süreleri özelleştirmesini](active-directory-b2c-token-session-sso.md) Azure AD B2C'de.

| Belirteç | Yaşam süresi | Açıklama |
| --- | --- | --- |
| Kimliği belirteçleri |Bir saat |Kimlik belirteçlerini bir saat için genellikle geçerlidir. Web uygulamanızın bu ömrü toomaintain kullanabilirsiniz (önerilen) kullanıcılar kendi oturumları. Ayrıca, farklı oturum yaşam süresi seçebilirsiniz. Uygulamanızı tooget yeni bir kimliği belirteci gerekirse, yeni bir oturum açma isteği tooAzure AD yalnızca toomake gerekir. Geçerli tarayıcı oturumu Azure AD ile bir kullanıcı varsa, o kullanıcı gerekli tooenter kimlik bilgilerini yeniden olmayabilir. |
| Yenileme belirteçlerini |Too14 günleri |Bir tek yenileme belirteci 14 gün sayısı için geçerli değil. Ancak, bir yenileme belirteci pek çok zaman geçersiz hale gelebilir. Uygulamanızı tootry toouse bir yenileme belirteci hello isteği başarısız kadar veya uygulamanızın hello yenileme belirteci ile yeni bir tane değiştirir kadar devam etmelidir. Bir yenileme belirteci hello kullanıcı son girilen kimlik bilgileri üzerinden 90 gün geçtiğinde, geçersiz olabilir. |
| Yetkilendirme kodları |Beş dakika |Yetkilendirme kodları bilerek ömürlüdür. Bunlar alındığında bunlar hemen erişim belirteçleri, kimlik belirteçlerini veya yenileme belirteçleri için kullanılan. |

