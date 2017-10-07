---
title: "Yetkilendirme kodu akışı - Azure AD B2C | Microsoft Docs"
description: "Nasıl toobuild web uygulamaları Azure AD B2C ve Openıd Connect kimlik doğrulama protokolünü kullanarak bilgi edinin."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: OAuth 2.0 yetkilendirme kodu akışı
Bir aygıt toogain tooprotected erişimine, web API'leri gibi yüklü uygulamalardaki hello OAuth 2.0 yetkilendirme kodu verme kullanabilirsiniz. OAuth 2.0 hello Azure Active Directory B2C (Azure AD B2C) uygulaması kullanarak ekleyebilirsiniz kaydolma, oturum açma ve diğer kimlik yönetimi tooyour mobil ve Masaüstü uygulamaları görevler. Bu makalede dilden bağımsızdır. Hello makalede, sizi tanımlamak nasıl toosend ve herhangi bir açık kaynak kitaplıkları kullanmadan HTTP iletileri alabilirsiniz.

<!-- TODO: Need link toolibraries -->

Merhaba OAuth 2.0 yetkilendirme kodu akışını açıklanan [4.1 hello OAuth 2.0 belirtimi bölüm](http://tools.ietf.org/html/rfc6749). Kimlik doğrulama ve yetkilendirme dahil olmak üzere çoğu uygulama türleri için kullandığınız [web uygulamaları](active-directory-b2c-apps.md#web-apps) ve [uygulamaları'yerel olarak yüklenen](active-directory-b2c-apps.md#mobile-and-native-apps). Merhaba OAuth 2.0 yetkilendirme kodu akışı toosecurely elde kullanabilirsiniz *erişim belirteçleri* , uygulamalarınız için olabilen tarafından güvenliği sağlanan kullanılan tooaccess kaynakları bir [yetkilendirme sunucusu](active-directory-b2c-reference-protocols.md#the-basics).

Bu makale üzerinde hello odaklanır **ortak istemcileri** OAuth 2.0 yetkilendirme kodu akışı. Ortak bir istemci, güvenilir toosecurely olamaz herhangi bir istemci uygulama gizli bir parola hello bütünlüğünü korumak olur. Bu, mobil uygulamaları, Masaüstü uygulamaları ve bir cihaz üzerinde çalışır ve tooget erişim belirteçleri gerekiyor temelde herhangi bir uygulama içerir. 

> [!NOTE]
> Azure AD B2C, kullanım kullanarak tooadd Kimlik Yönetimi tooa web uygulaması [Openıd Connect](active-directory-b2c-reference-oidc.md) OAuth 2.0 yerine.

Azure AD B2C hello standart OAuth 2.0 akar toodo Basit kimlik doğrulama ve yetkilendirme'den fazla genişletir. Merhaba tanıtır [İlkesi parametresi](active-directory-b2c-reference-policies.md). Yerleşik ilkeleri ile tooadd kullanıcı deneyimleri tooyour uygulama gibi OAuth 2.0 kullanabileceğiniz kaydolma, oturum açma ve profil yönetimi. Bu makalede, nasıl gösteriyoruz her birinde karşılaştığında yerel uygulamalarınızda toouse OAuth 2.0 ve ilkeleri tooimplement. Ayrıca nasıl tooget erişim belirteçleri erişmek için API web gösteriyoruz.

Bizim örnek Azure AD B2C dizini kullanırız Hello örnek HTTP isteklerinde bu makalede, **fabrikamb2c.onmicrosoft.com**. Ayrıca bizim örnek uygulama ve ilkeleri kullanırız. Bu değerleri kullanarak kendiniz hello istekleri deneyebilir ya da kendi değerlerinizle değiştirin.
Nasıl çok öğrenin[kendi Azure AD B2C dizini, uygulama ve ilkeleri alma](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Bir yetkilendirme kodu alın
Merhaba yetkilendirme kodu akışı başlar hello kullanıcı toohello yönlendirerek hello istemcisiyle `/authorize` uç noktası. Bu hello etkileşimli hello akış burada hello kullanıcı eylemde parçasıdır. Bu istekte hello istemci hello gösterir `scope` parametresi hello izinleri hello kullanıcıdan tooacquire gerekiyor. Merhaba, `p` parametresi hello İlkesi tooexecute gösterir. Merhaba aşağıdaki üç örnekler (okunabilirlik için satır sonuyla) her başka bir ilke kullanın.

### <a name="use-a-sign-in-policy"></a>Bir oturum açma ilkesini kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Kayıt İlkesi'ni kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Bir profili Düzenle ilkesini kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| client_id |Gerekli |Merhaba uygulama kimliği atanan hello tooyour uygulamada [Azure portal](https://portal.azure.com). |
| response_type |Gerekli |içermelidir hello yanıt türü `code` hello yetkilendirme kodu akışı. |
| redirect_uri |Gerekli |Merhaba, uygulamanız tarafından alınan kimlik doğrulama yanıtları nereden gönderildiğini ve uygulamanızı URI'sini yeniden yönlendir. URL kodlanmış olmalıdır dışında tam olarak hello yeniden yönlendirme hello Portalı'nda kayıtlı URI'ler biriyle eşleşmelidir. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi. Tek bir kapsam değeri tooAzure Active Directory (Azure AD) her iki talep edilen hello izinleri gösterir. Uygulamanızın kendi hizmeti veya web API'si karşı kullanılabilir bir erişim belirteci gerektiğini hello kapsam anlaşılacağı gibi kimliği temsil ettiği hello istemcisini kullanarak hello aynı istemci kimliği  Merhaba `offline_access` kapsamını belirtir, uygulamanız için uzun süreli erişim tooresources bir yenileme belirteci gerekiyor. Merhaba de kullanabilirsiniz `openid` kapsam toorequest Azure AD B2C kimliği belirtecinden. |
| response_mode |Önerilen |Merhaba yöntemi toosend hello elde edilen yetkilendirme kodu geri tooyour uygulama kullanın. Bu olabilir `query`, `form_post`, veya `fragment`. |
| durum |Önerilen |Merhaba belirteci yanıtta döndürülen hello istekte bulunan bir değer. Toouse istediğiniz herhangi bir içerik dizesi olabilir. Genellikle, rastgele oluşturulmuş bir benzersiz değer kullanılır, tooprevent siteler arası istek sahteciliği saldırılarına. Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. Örneğin, hello sayfa hello kullanıcı açıktı veya yürütülmekte olan ilke hello. |
| P |Gerekli |yürütülen hello ilkesi. Buna ait hello Azure AD B2C dizininizde oluşturulan bir ilkenin adını. Hello ilkesi adı değeri ile başlamalıdır **b2c\_1\_**. toolearn ilkeleri hakkında daha fazla bilgi görmek [Azure AD B2C yerleşik ilkeleri](active-directory-b2c-reference-policies.md). |
| istemi |İsteğe bağlı |gerekli bir kullanıcı etkileşimi Hello türü. Şu anda hello tek geçerli değer: `login`, hangi kullanıcıların kimlik bilgilerini bu isteğin zorlar hello kullanıcı tooenter. Çoklu oturum açma etkili olmaz. |

Bu noktada, hello kullanıcı toocomplete hello İlkesi'nin iş akışı istedi. Bu, kullanıcı adını ve parolasını girerek hello kullanıcı hello dizin ya da başka bir sayıyı adımları için kaydolan bir sosyal kimlik bilgilerinizle oturum gerektirebilir. Kullanıcı eylemlerini hello İlkesi nasıl tanımlandığına bağlıdır.

Merhaba kullanıcı hello İlkesi tamamlandıktan sonra Azure AD bir yanıt tooyour uygulaması için kullanılan hello değerde döndürür `redirect_uri`. Hello belirtilen hello yöntemini kullanır `response_mode` parametresi. Merhaba yanıt olan tam olarak hello aynı her hello kullanıcı eylemi senaryoları, yürütülen hello İlkesi bağımsız için.

Kullanan başarılı yanıt `response_mode=query` şöyle görünür:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Parametre | Açıklama |
| --- | --- |
| Kod |İstenen uygulama hello hello yetkilendirme kodu. Merhaba uygulama için bir hedef kaynak hello yetkilendirme kodu toorequest bir erişim belirteci kullanabilirsiniz. Yetkilendirme kodları çok kısa ömürlüdür. Genellikle, yaklaşık 10 dakika sonra süresi. |
| durum |Önceki bölümde hello hello tablosunda Hello tam açıklamasına bakın. Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama bu hello doğrulamalısınız `state` hello istek ve yanıt değerler aynı. |

Böylece Hello uygulama bunları uygun şekilde işleyebilir hata yanıtları toohello yeniden yönlendirme URI'si da gönderilebilir:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametre | Açıklama |
| --- | --- |
| error |Tooclassify hello oluşan hataları türlerini kullanabilirsiniz bir hata kodu dizesi. Merhaba dize tooreact tooerrors de kullanabilirsiniz. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| durum |Tablo önceki hello Hello tam açıklamaya bakın. Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama bu hello doğrulamalısınız `state` hello istek ve yanıt değerler aynı. |

## <a name="2-get-a-token"></a>2. Belirteç alın
Bir yetkilendirme kodu edindiğiniz, hello kullanmak `code` bir POST isteği toohello göndererek kaynak belirteci toohello amaçlar için `/token` uç noktası. Azure AD B2C'de hello için bir belirteç isteyebileceği yalnızca uygulamanın kendi arka uç web API kaynaktır. belirteç tooyourself istemek için kullanılan hello uygulamanızın istemci kimliği, hello kapsamı olarak toouse kuraldır:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| P |Gerekli |Merhaba, kullanılan tooacquire hello yetkilendirme ilkesi kodu. Bu isteği başka bir ilke kullanamazsınız. Bu parametre toohello eklediğiniz Not *sorgu dizesi*, hello POST gövdesi içinde değil. |
| client_id |Gerekli |Merhaba uygulama kimliği atanan hello tooyour uygulamada [Azure portal](https://portal.azure.com). |
| grant_type |Gerekli |grant Hello türü. Merhaba yetkilendirme kodu akışı için hello grant türü olmalıdır `authorization_code`. |
| Kapsam |Önerilen |Kapsamları boşlukla ayrılmış listesi. Tek bir kapsam değeri tooAzure AD her iki talep edilen hello izinleri gösterir. Uygulamanızın kendi hizmeti veya web API'si karşı kullanılabilir bir erişim belirteci gerektiğini hello kapsam anlaşılacağı gibi kimliği temsil ettiği hello istemcisini kullanarak hello aynı istemci kimliği  Merhaba `offline_access` kapsamını belirtir, uygulamanız için uzun süreli erişim tooresources bir yenileme belirteci gerekiyor.  Merhaba de kullanabilirsiniz `openid` kapsam toorequest Azure AD B2C kimliği belirtecinden. |
| Kod |Gerekli |Merhaba akışının hello ilk leg aldığınız hello yetkilendirme kodu. |
| redirect_uri |Gerekli |Merhaba hello yetkilendirme kodu aldığınız hello uygulama URI'sini yeniden yönlendir. |

Başarılı bir token yanıt şöyle görünür:

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
| token_type |Merhaba belirteç türü değeri. Merhaba yalnızca yazın Azure AD desteklediği taşıyıcı biçimde. |
| access_token |Merhaba, JSON Web Token (istediğiniz JWT) imzalanmış. |
| Kapsam |belirteç hello hello kapsamlar için geçerlidir. Kapsamları toocache belirteçleri daha sonra kullanmak üzere de kullanabilirsiniz. |
| expires_in |Merhaba belirteci hello süre uzunluğu (saniye olarak) geçerli değil. |
| refresh_token |Bir OAuth 2.0 yenileme belirteci. Merhaba geçerli belirteç süresi dolduktan sonra bu belirteci tooacquire ek belirteçler hello uygulamasını kullanabilir. Yenileme belirteçleri uzun süreli. Bunları tooretain erişim tooresources uzun süre için kullanabilirsiniz. Daha fazla bilgi için bkz: Merhaba [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). |

Hata yanıtları şöyle görünür:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametre | Açıklama |
| --- | --- |
| error |Tooclassify hello oluşan hataları türlerini kullanabilirsiniz bir hata kodu dizesi. Merhaba dize tooreact tooerrors de kullanabilirsiniz. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

## <a name="3-use-hello-token"></a>3. Merhaba belirteci kullanın
Bir erişim belirteci başarıyla edindiğiniz, hello belirteç isteklerini tooyour arka uç web API'leri hello dahil ederek kullanabileceğiniz `Authorization` üstbilgisi:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Merhaba belirtecini yenileme
Erişim belirteçleri ve kimlik belirteçlerini ömürlüdür. Zaman aşımına uğradığında toocontinue tooaccess kaynakları yenilemeniz gerekir. toodo Bu, başka bir POST isteği toohello gönderme `/token` uç noktası. Bu süre, hello sağlamak `refresh_token` hello yerine `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| P |Gerekli |kullanılan tooacquire hello özgün yenileme belirteci olan hello ilkesi. Bu isteği başka bir ilke kullanamazsınız. Bu parametre toohello eklediğiniz Not *sorgu dizesi*, hello POST gövdesi içinde değil. |
| client_id |Önerilen |Merhaba uygulama kimliği atanan hello tooyour uygulamada [Azure portal](https://portal.azure.com). |
| grant_type |Gerekli |grant Hello türü. Bu hello yetkilendirme kodu akışını Bacak için hello grant türü olmalıdır `refresh_token`. |
| Kapsam |Önerilen |Kapsamları boşlukla ayrılmış listesi. Tek bir kapsam değeri tooAzure AD her iki talep edilen hello izinleri gösterir. Uygulamanızın kendi hizmeti veya web API'si karşı kullanılabilir bir erişim belirteci gerektiğini hello kapsam anlaşılacağı gibi kimliği temsil ettiği hello istemcisini kullanarak hello aynı istemci kimliği  Merhaba `offline_access` kapsamını belirtir, uygulamanız için uzun süreli erişim tooresources bir yenileme belirteci gerekir.  Merhaba de kullanabilirsiniz `openid` kapsam toorequest Azure AD B2C kimliği belirtecinden. |
| redirect_uri |İsteğe bağlı |Merhaba hello yetkilendirme kodu aldığınız hello uygulama URI'sini yeniden yönlendir. |
| refresh_token |Gerekli |Merhaba akışının hello ikinci leg edindiğiniz hello özgün yenileme belirteci. |

Başarılı bir token yanıt şöyle görünür:

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
| token_type |Merhaba belirteç türü değeri. Merhaba yalnızca yazın Azure AD desteklediği taşıyıcı biçimde. |
| access_token |Merhaba, istenen JWT imzalanmış. |
| Kapsam |belirteç hello hello kapsamlar için geçerlidir. Merhaba kapsamları toocache belirteçleri daha sonra kullanmak üzere de kullanabilirsiniz. |
| expires_in |Merhaba belirteci hello süre uzunluğu (saniye olarak) geçerli değil. |
| refresh_token |Bir OAuth 2.0 yenileme belirteci. Merhaba geçerli belirteç süresi dolduktan sonra bu belirteci tooacquire ek belirteçler hello uygulamasını kullanabilir. Yenileme belirteçlerini uzun süreli ve uzun süre için kullanılan tooretain erişim tooresources olabilir. Daha fazla bilgi için bkz: Merhaba [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). |

Hata yanıtları şöyle görünür:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları tooclassify türlerini kullanabilirsiniz bir hata kodu dizesi. Merhaba dize tooreact tooerrors de kullanabilirsiniz. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Kendi Azure AD B2C dizini kullanın
Bu istekleri kendiniz aşağıdaki tam hello tootry adımları. Bu makalede, kendi değerlerle kullandık hello örnek değerleri değiştirin.

1. [Azure AD B2C dizini oluşturma](active-directory-b2c-get-started.md). Merhaba istekleri dizininizde hello adını kullanın.
2. [Uygulama oluşturma](active-directory-b2c-app-registration.md) tooobtain bir uygulama kimliği ve yeniden yönlendirme URI'si. Yerel istemci uygulamanızı içerir.
3. [İlkelerinizi oluşturma](active-directory-b2c-reference-policies.md) tooobtain ilke adları.

