---
title: "Azure Active Directory B2C: örtük akışını kullanarak tek sayfa uygulamaları | Microsoft Docs"
description: "Nasıl toobuild tek sayfa uygulamaları doğrudan OAuth 2.0 örtük kullanarak Azure Active Directory B2C ile akış öğrenin."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C: Tek sayfalı uygulama oturum OAuth 2.0 örtük akışını kullanarak açma

> [!NOTE]
> Bu özelliğin önizlemede değil.
> 

Birçok modern uygulamanın, JavaScript'te öncelikli olarak yazılmış tek sayfa uygulaması ön ucu sahip. Genellikle, hello uygulama çerçevesi AngularJS, Ember.js veya Durandal gibi kullanılarak yazılır. Tek sayfalı uygulamalar ve öncelikle tarayıcıda çalışan diğer JavaScript uygulamalar kimlik doğrulaması için ek bazı zorluklar vardır:

* Bu uygulamaları Hello güvenlik özelliklerini geleneksel sunucu tabanlı web uygulamalarından önemli ölçüde farklıdır.
* Çok sayıda yetkilendirme sunucularını ve kimlik sağlayıcıları çıkış noktaları arası kaynak paylaşma (CORS) isteklerini desteklemez.
* Tam sayfa tarayıcı yeniden yönlendirmeleri hello uygulama çıktığınızda önemli ölçüde bozucu toohello kullanıcı deneyimi olabilir.

toosupport bu uygulamaları, Azure Active Directory B2C (Azure AD B2C) hello OAuth 2.0 örtük akışını kullanır. Merhaba OAuth 2.0 yetkilendirme örtük grant akış açıklanan [4.2 hello OAuth 2.0 belirtimi bölüm](http://tools.ietf.org/html/rfc6749). Örtük akışını hello uygulama belirteçlerini doğrudan hello alır Azure Active Directory (Azure AD) kimlik doğrulama uç noktası, herhangi bir sunucudan sunucuya exchange olmadan. Tüm kimlik doğrulaması mantığı ve gerçekleştirilen işlemlerin işleme oturumu tamamen ek sayfa yeniden yönlendirmeleri olmadan hello JavaScript istemci yerleştirin.

Azure AD B2C hello standart OAuth 2.0 örtük akışını toomore daha basit kimlik doğrulama ve yetkilendirme genişletir. Azure AD B2C tanıtır hello [İlkesi parametresi](active-directory-b2c-reference-policies.md). Hello İlkesi parametresiyle tooadd kullanıcı deneyimleri tooyour uygulama gibi OAuth 2.0 kullanabilirsiniz kaydolma, oturum açma ve profil yönetimi. Bu makalede, toouse nasıl hello örtük akış ve Azure AD tooimplement her bu deneyimler, tek sayfalı uygulamalarınızda gösteriyoruz. başlamanıza, toohelp ele göz atın bizim [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) ve [Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) örnekleri.

Bizim örnek Azure AD B2C dizini kullanırız Hello örnek HTTP isteklerinde bu makalede, **fabrikamb2c.onmicrosoft.com**. Ayrıca kendi örnek uygulama ve ilkeleri kullanırız. Bu değerleri kullanarak kendiniz hello istekleri deneyebilir ya da kendi değerlerinizle değiştirin.
Nasıl çok öğrenin[kendi Azure AD B2C dizini, uygulama ve ilkeleri alma](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Protokol diyagramı

oturum açma Hello örtük akış aşağıdaki şekilde hello şöyle görünür. Her adım ayrıntılı hello makalenin sonraki bölümlerinde açıklanmıştır.

![Openıd Connect kulvarları](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Kimlik doğrulama isteklerini gönderme
Web uygulamanızı tooauthenticate hello kullanıcı gerekir ve bir ilke yürütme zaman hello kullanıcı toohello yönlendirir `/authorize` uç noktası. Bu hello etkileşimli hello akış burada hello kullanıcı, hello ilkesine bağlı olarak eylemde bölümüdür. Merhaba kullanıcı kimliği hello Azure AD uç noktasından belirteç alır.

Bu istekte hello istemci hello gösterir `scope` parametresi hello izinleri hello kullanıcıdan tooacquire gerekiyor. Merhaba, `p` parametresi hello İlkesi tooexecute gösterir. Merhaba aşağıdaki üç örnekler (okunabilirlik için satır sonuyla) her başka bir ilke kullanın. tooget bir fikir her istek işleyişi için bir tarayıcı ile çalışan yapıştırma hello isteği deneyin.

### <a name="use-a-sign-in-policy"></a>Bir oturum açma ilkesini kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Kayıt İlkesi'ni kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Bir profili Düzenle ilkesini kullanın
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| client_id |Gerekli |Merhaba uygulama kimliği atanan hello tooyour uygulamada [Azure portal](https://portal.azure.com). |
| response_type |Gerekli |İçermelidir `id_token` Openıd Connect oturum açma için. Merhaba yanıt türü içerebilir `token`. Kullanırsanız `token`, uygulamanızı hello hemen bir erişim belirteci alabilir uç noktası, son noktanın yetkilendirilmesi ikinci bir istek toohello yapmadan yetkilendirin.  Merhaba kullanırsanız `token` yanıt türü, hello `scope` parametresi için hangi kaynak tooissue hello belirtecini gösteren bir kapsam içermesi gerekir. |
| redirect_uri |Önerilen |Merhaba burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan uygulamanızı URI'sini yeniden yönlendir. URL kodlanmış olmalıdır dışında tam olarak hello yeniden yönlendirme hello Portalı'nda kayıtlı URI'ler biriyle eşleşmelidir. |
| response_mode |Önerilen |Merhaba yöntemi toouse toosend hello elde edilen belirteci geri tooyour uygulama belirtir.  Örtük akışlar için kullanmak `fragment`. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi. Tek bir kapsam değeri tooAzure AD her iki talep edilen hello izinleri gösterir. Merhaba `openid` kapsam kimliği belirteçleri hello biçiminde hello kullanıcı hakkında hello kullanıcı ve get verilerdeki izni toosign gösterir. (Biz bu konuda daha sonra hello makalesinde konuşun.) Merhaba `offline_access` kapsamı web uygulamaları için isteğe bağlı değil. Uygulamanızın uzun süreli erişim tooresources için bir yenileme belirteci gerektiğini belirtir. |
| durum |Önerilen |Merhaba, aynı zamanda isteğinde bir değer hello belirteci yanıt olarak döndürülür. Toouse istediğiniz herhangi bir içerik dizesi olabilir. Genellikle, rastgele oluşturulmuş, benzersiz bir değer kullanılır, tooprevent siteler arası istek sahteciliği saldırılarına. Merhaba ayrıca kullanılan tooencode bilgi durumudur hello kimlik doğrulama isteği oluşmadan önce hello uygulamasında hello kullanıcının durumu hakkında gibi hello sayfası üzerinde oldukları. |
| nonce |Gerekli |İstekteki hello elde edilen kimliği belirteç talep olarak dahil edilen (Merhaba uygulama tarafından oluşturulan) hello dahil bir değer. Merhaba uygulama daha sonra bu değeri toomitigate belirteç yeniden yürütme saldırılarına doğrulayabilirsiniz. Genellikle, kullanılan tooidentify hello kaynak hello isteğinin olabilir rastgele, benzersiz bir dize hello değerdir. |
| P |Gerekli |Hello İlkesi tooexecute. Hello Azure AD B2C kiracınızda oluşturulan bir ilkenin adını. Hello ilkesi adı değeri ile başlamalıdır **b2c\_1\_**. Daha fazla bilgi için bkz: [Azure AD B2C yerleşik ilkeleri](active-directory-b2c-reference-policies.md). |
| istemi |İsteğe bağlı |gerekli olan bir kullanıcı etkileşimi Hello türü. Şu anda hello tek geçerli değer: `login`. Bu hello kullanıcı tooenter kimlik bilgilerini bu isteği zorlar. Çoklu oturum açma etkili olmaz. |

Bu noktada, hello kullanıcı toocomplete hello İlkesi'nin iş akışı istedi. Bu, kullanıcı adını ve parolasını girerek hello kullanıcı hello dizin ya da başka bir sayıyı adımları için kaydolan bir sosyal kimlik bilgilerinizle oturum gerektirebilir. Kullanıcı eylemlerini hello İlkesi nasıl tanımlandığına bağlıdır.

Merhaba kullanıcı hello İlkesi tamamlandıktan sonra Azure AD bir yanıt tooyour uygulaması için kullanılan hello değerde döndürür `redirect_uri`. Hello belirtilen hello yöntemini kullanır `response_mode` parametresi. Merhaba yanıt olan tam olarak hello aynı her hello kullanıcı eylemi senaryoları, yürütülen hello İlkesi bağımsız için.

### <a name="successful-response"></a>Başarılı yanıt
Kullanan başarılı yanıt `response_mode=fragment` ve `response_type=id_token+token` okunabilirliği için satır sonu ile Merhaba aşağıdaki gibi görünür:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| Parametre | Açıklama |
| --- | --- |
| access_token |İstenen uygulama hello hello erişim belirteci.  Merhaba erişim belirteci kodunu çözdü veya gerekir aksi takdirde sahip denetlenir. Genel olmayan bir dize olarak işlenebilir. |
| token_type |Merhaba belirteç türü değeri. Merhaba yalnızca yazın Azure AD desteklediği taşıyıcı biçimde. |
| expires_in |erişim belirteci hello süre Hello uzunluğu (saniye olarak) geçerli değil. |
| Kapsam |belirteç hello hello kapsamlar için geçerlidir. Kapsamları toocache belirteçleri daha sonra kullanmak üzere de kullanabilirsiniz. |
| id_token |İstenen uygulama hello kimliği belirteci hello. Merhaba kullanıcıyla oturumu başlatmak ve hello kimliği belirteci tooverify hello kullanıcının kimliğini kullanın. Merhaba kimlik belirteçlerini ve içerikleri hakkında daha fazla bilgi için bkz: [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). |
| durum |Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama bu hello doğrulamalısınız `state` hello istek ve yanıt değerler aynı. |

### <a name="error-response"></a>Hata yanıtı
Böylece Hello uygulama bunları uygun şekilde işleyebilir hata yanıtları toohello yeniden yönlendirme URI'si da gönderilebilir:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametre | Açıklama |
| --- | --- |
| error |Bir hata kodu dizesi oluşan hataları tooclassify türleri kullanılır. Merhaba hata kodunu hata işleme için de kullanabilirsiniz. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |
| durum |Tablo önceki hello Hello tam açıklamaya bakın. Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama bu hello doğrulamalısınız `state` hello istek ve yanıt değerler aynı.|

## <a name="validate-hello-id-token"></a>Merhaba kimliği belirtecini doğrula
Bir kimliği belirteci alma yeterli tooauthenticate hello kullanıcı değil. Merhaba kimliği belirtecin imzayı doğrulamak ve uygulamanızın gereksinimleri başına hello belirtecindeki hello talep doğrulamanız gerekir. Azure AD B2C kullanan [JSON Web belirteçleri (Jwt'ler)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) ve ortak anahtar şifrelemesi toosign belirteçleri ve geçerli olduğunu doğrulayın.

Birçok açık kaynak kitaplıkları Jwt'ler doğrulamak için kullanılabilen, hello dil bağlı olarak toouse tercih eder. Kendi doğrulama mantığı uygulamak yerine kullanılabilir açık kaynak kitaplıkları keşfetme göz önünde bulundurun. Merhaba bilgileri kullanabilirsiniz Bu makale toohelp tooproperly bu kitaplıklarını nasıl kullanacağınızı öğrenin.

Azure AD B2C Openıd Connect meta veri son nokta vardır. Bir uygulama çalışma zamanında hello uç nokta toofetch Azure AD B2C bilgilerini kullanabilirsiniz. Bu bilgiler, uç noktaları, belirteç içerikleri ve belirteç imzalama anahtarları içerir. Azure AD B2C kiracınızda her ilke için bir JSON meta veri belgesi yoktur. Örneğin, hello meta veri belgesi hello b2c_1_sign_in İlkesi'nde hello fabrikamb2c.onmicrosoft.com Kiracı için aşağıdaki konumda bulunur:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Bu yapılandırma belgenin hello özellikleri biri hello `jwks_uri`. aynı ilke olacaktır hello Hello değeri:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

hangi ilke kullanılan toosign kimliği belirteci oluştu (ve burada toofetch hello meta verileri), toodetermine iki seçeneğiniz vardır. Hello ilkesi adı hello ilk olarak dahil `acr` içinde talep `id_token`. Merhaba nasıl tooparse hello kimliği belirtecinden talepleri hakkında daha fazla bilgi için bkz [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md). Diğer seçeneğiniz tooencode hello hello hello değeri ilkedir `state` hello isteği gönderdiğinizde parametresi. Ardından, hello kod çözme `state` parametresi toodetermine ilkeyi kullanıldı. Her iki yöntem geçerli değil.

Merhaba meta veri belgesi hello Openıd Connect meta veri uç noktasından edindiğiniz sonra hello RSA-256 (Bu uç noktada bulunur) ortak anahtarları toovalidate hello hello kimliği belirtecinin imzası kullanabilirsiniz. Belirli bir zamanda Bu uç noktada listelenen birden çok anahtar olabilir, her tarafından tanımlanan bir `kid`. Merhaba üstbilgisinin `id_token` de içeren bir `kid` talep. Bu anahtarların kullanılan toosign hello kimliği belirteci olduğu belirtir. Hakkında bilgi dahil daha fazla bilgi için [belirteçleri doğrulama](active-directory-b2c-reference-tokens.md#token-validation), hello bkz [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

Merhaba kimliği belirtecinin hello imzası doğrulama sonra birkaç talep doğrulama gerektirir. Örneğin:

* Merhaba doğrulamak `nonce` tooprevent belirteç yeniden yürütme saldırılarını talep. Oturum açma hello istekte belirtilen değeri olmalıdır.
* Merhaba doğrulamak `aud` kimliği belirteci hello tooensure, uygulamanız için yayımlandığında talep. Değeri, uygulamanızın hello uygulama kimliği olmalıdır.
* Merhaba doğrulamak `iat` ve `exp` talep kimliği belirteci hello tooensure süresi.

Gerçekleştirmeniz gereken birkaç daha fazla doğrulama hello ayrıntılı açıklanan [Openıd Connect çekirdek Spec](http://openid.net/specs/openid-connect-core-1_0.html). Senaryonuza bağlı olarak toovalidate ek talepleri de isteyebilirsiniz. Bazı ortak doğrulamaları şunları içerir:

* Bu hello kullanıcıya veya kuruluşa sağlama hello uygulaması için kaydolmuş.
* Merhaba kullanıcının uygun yetkilendirme ve ayrıcalıklara sahip olma.
* Belirli bir kimlik doğrulama gücünü oluştuğunu gibi Azure çok faktörlü kimlik doğrulamasını kullanarak gibi sağlama.

Merhaba hello talep kimliği belirteci hakkında daha fazla bilgi için bkz: [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md).

Merhaba kimliği belirteci tamamen doğrulandıktan sonra bir oturum hello kullanıcıyla başlayabilirsiniz. Uygulamanızda hello talep hello kimliği belirteci tooobtain hello kullanıcı bilgilerini kullanın. Bu bilgiler, görüntü, kayıtları, yetkilendirme ve benzeri için kullanılabilir.

## <a name="get-access-tokens"></a>Erişim belirteci alın
Merhaba tek şey, web uygulamaları gereksinimlerini toodo olan ilkeleri yürütüyorsa atlayabilirsiniz hello sonraki birkaç bölümler. Kimliği doğrulanmış toomake çağrıları tooa web API gerekir ve hangi Azure AD B2C tarafından korunan geçerli yalnızca tooweb uygulamalar bölümleri aşağıdaki hello Hello bilgileri var.

Tooyour tek sayfalı uygulama hello kullanıcı oturum açtığınız, çağrıyı yapan web Azure AD tarafından güvenliği sağlanan API'leri için erişim belirteçleri alabilir. Zaten bir belirteç hello kullanarak aldığınız olsa bile `token` yanıt türü kullanabileceğiniz bu yöntem tooacquire belirteçleri için ek kaynaklar hello kullanıcı toosign yeniden yönlendirme olmadan.

Tipik web uygulama akışı isteği toohello yaparak bunu `/token` uç noktası.  Ancak, hello endpoint AJAX yapma tooget çağırır ve yenileme belirteçleri bir seçenek değil değil destek CORS isteklerini desteklemez. Bunun yerine, bir gizli HTML iframe öğesi tooget yeni belirteçleri hello örtük akış diğer web API'leri kullanabilirsiniz. İle okunabilirliği için satır sonu, örnek aşağıda verilmiştir:

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| client_id |Gerekli |Merhaba uygulama kimliği atanan hello tooyour uygulamada [Azure portal](https://portal.azure.com). |
| response_type |Gerekli |İçermelidir `id_token` Openıd Connect oturum açma için.  Merhaba yanıt türü içerebilir `token`. Kullanırsanız `token` Burada, uygulamanızın hemen bir erişim belirteci hello alabilir uç noktası, son noktanın yetkilendirilmesi ikinci bir istek toohello yapmadan yetkilendirin. Merhaba kullanırsanız `token` yanıt türü, hello `scope` parametresi için hangi kaynak tooissue hello belirtecini gösteren bir kapsam içermesi gerekir. |
| redirect_uri |Önerilen |Merhaba burada kimlik doğrulama yanıtları gönderilebilen veya uygulamanız tarafından alınan uygulamanızı URI'sini yeniden yönlendir. URL kodlanmış olmalıdır dışında tam olarak hello yeniden yönlendirme hello Portalı'nda kayıtlı URI'ler biriyle eşleşmelidir. |
| Kapsam |Gerekli |Kapsamları boşlukla ayrılmış listesi.  Belirteçleri almak için hedeflenen hello kaynak için ihtiyaç duyduğunuz tüm kapsamlar içerir. |
| response_mode |Önerilen |Kullanılan toosend hello elde edilen belirteci geri tooyour uygulaması hello yöntemini belirtir.  Olabilir `query`, `form_post`, veya `fragment`. |
| durum |Önerilen |Merhaba belirteci yanıtta döndürülen hello istekte bulunan bir değer.  Toouse istediğiniz herhangi bir içerik dizesi olabilir.  Genellikle, rastgele oluşturulmuş, benzersiz bir değer kullanılır, tooprevent siteler arası istek sahteciliği saldırılarına.  Hello kimlik doğrulama isteği oluşmadan önce hello durumu ayrıca kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. Örneğin, hello sayfa veya Görünüm hello kullanıcı açıktı. |
| nonce |Gerekli |Merhaba elde edilen kimliği belirteç talep olarak dahil edilen hello uygulama tarafından üretilen hello isteğinde bulunan bir değer.  Merhaba uygulama daha sonra bu değeri toomitigate belirteç yeniden yürütme saldırılarına doğrulayabilirsiniz. Genellikle, hello isteği hello kaynağını tanımlayan rastgele, benzersiz bir dize hello değerdir. |
| istemi |Gerekli |Gizli bir iframe toorefresh ve get belirteçleri kullanın `prompt=none` IFRAME hello tooensure hello oturum açma sayfasında takılı değil ve hemen döndürür. |
| login_hint |Gerekli |Gizli bir iframe toorefresh ve get belirteçlerinde hello kullanıcı belirli bir zamanda sahip birden çok oturumlar arasında bu ipucu toodistinguish hello kullanıcı hello kullanıcı adını içerir. Hello kullanarak bir önceki oturum bileşeninden hello kullanıcıadı ayıklayabilirsiniz `preferred_username` talep. |
| domain_hint |Gerekli |Olabilir `consumers` veya `organizations`.  Yenileme ve gizli bir iframe içinde belirteçleri almak için hello içermelidir `domain_hint` hello istekteki değeri.  Merhaba ayıklamak `tid` hello kimliği belirtecinden bir önceki oturum açma toodetermine, hangi değer toouse talep.  Merhaba, `tid` değer talep `9188040d-6c67-4c5b-b112-36a304b66dad`, kullanmak `domain_hint=consumers`.  Aksi takdirde kullanın `domain_hint=organizations`. |

Merhaba ayarı tarafından `prompt=none` parametresi, bu istek ya da başarılı ya da hemen başarısız olur ve tooyour uygulama döndürür.  Başarılı yanıt tooyour uygulama gönderilen belirtilen hello, hello belirtilen hello yöntemi kullanarak yeniden yönlendirme URI'si `response_mode` parametresi.

### <a name="successful-response"></a>Başarılı yanıt
Kullanarak başarılı bir yanıt `response_mode=fragment` şöyle görünür:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Parametre | Açıklama |
| --- | --- |
| access_token |İstenen uygulama hello hello belirteci. |
| token_type |Merhaba belirteç türü her zaman taşıyıcı olacaktır. |
| durum |Varsa bir `state` parametresi dahil hello istekte hello aynı değere hello yanıt olarak görünmelidir. Merhaba uygulama bu hello doğrulamalısınız `state` hello istek ve yanıt değerler aynı. |
| expires_in |Ne kadar süreyle hello erişim belirteci (saniye olarak) geçerli değil. |
| Kapsam |erişim belirteci hello hello kapsamlar için geçerlidir. |

### <a name="error-response"></a>Hata yanıtı
Böylece Hello uygulama bunları uygun şekilde işleyebilir hata yanıtları toohello yeniden yönlendirme URI'si da gönderilebilir.  İçin `prompt=none`, beklenen hata şöyle görünür:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parametre | Açıklama |
| --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir bir hata kodu dizesi. Merhaba dize tooreact tooerrors de kullanabilirsiniz. |
| error_description |Yardımcı olabilecek belirli bir hata iletisi kimlik doğrulama hatası hello kök nedenini tanımlayın. |

Merhaba IFRAME istekte bu hatayı alırsanız hello kullanıcı etkileşimli olarak yeniden tooretrieve içinde yeni bir belirteç oturum açmanız gerekir. Bu, uygulamanız için anlamlı bir şekilde işleyebilir.

## <a name="refresh-tokens"></a>Yenileme belirteçlerini
Kimlik belirteçlerini ve erişim belirteçleri kısa bir süre sonra süresi dolacak. Uygulamanızı belirteçleri almak için düzenli aralıklarla, bunlar toorefresh hazırlanması gerekir.  belirteç, her iki tür toorefresh gerçekleştirmek hello kullandık bir önceki örnekte hello kullanarak aynı gizli IFRAME isteği `prompt=none` parametresi toocontrol Azure AD adımları.  Yeni bir tooreceive `id_token` emin toouse olması, değer `response_type=id_token` ve `scope=openid`ve bir `nonce` parametresi.

## <a name="send-a-sign-out-request"></a>Oturum kapatma isteği gönder
Merhaba uygulama dışında toosign hello kullanıcı istediğinizde hello kullanıcı tooAzure AD toosign çıkışı yönlendirin. Bunu yapmazsanız, hello kullanıcı kimlik bilgilerini yeniden girmeden mümkün tooreauthenticate tooyour uygulama olabilir. Bu durum, geçerli tek bir oturum açma oturumu Azure AD ile gerekir çünkü.

Merhaba kullanıcı toohello yalnızca yönlendirebilirsiniz `end_session_endpoint` yani aynı Openıd Connect meta veri belgesi açıklanan listelenen hello [doğrulama hello kimliği belirteci](#validate-the-id-token). Örneğin:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parametre | Gerekli mi? | Açıklama |
| --- | --- | --- |
| P |Gerekli |Hello İlkesi toouse toosign hello kullanıcı uygulamanızı dışında. |
| post_logout_redirect_uri |Önerilen |Merhaba hello kullanıcının yeniden yönlendirilen tooafter başarılı olmalıdır oturum kapatma. Dahil edilmezse, Azure AD B2C Genel ileti toohello kullanıcı görüntüler. |

> [!NOTE]
> Merhaba kullanıcı toohello yönlendirerek `end_session_endpoint` bazı Azure AD B2C ile Merhaba kullanıcının tek oturum açma durumu temizler. Ancak, hello kullanıcının sosyal kimlik sağlayıcısı oturumunu dışında hello kullanıcı oturum değil. Merhaba kullanıcı hello seçerse aynı sağlayıcısı bir sonraki oturum açma sırasında tanımlamak, hello kullanıcı, kimlik bilgilerini girmeden kimlik doğrulaması yeniden yapılır. Bir kullanıcı Azure AD B2C uygulamanızı dışında toosign isterse, mutlaka toocompletely oturum Facebook hesaplarında dışında örneğin istedikleri anlamına gelmez. Ancak, yerel hesaplar için hello kullanıcının oturumunu düzgün sonlandırılır.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Kendi Azure AD B2C kiracısı kullanın
Bunlar kendiniz isteklerini tamamlamak tootry aşağıdaki üç adımları hello. Bu makalede, kendi değerlerle kullanırız hello örnek değerleri değiştirin:

1. [Bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md). Merhaba istekleri kiracınızda hello adını kullanın.
2. [Uygulama oluşturma](active-directory-b2c-app-registration.md) tooobtain bir uygulama kimliği ve `redirect_uri` değeri. Bir web uygulaması veya web API uygulamanızı içerir. İsteğe bağlı olarak, bir uygulama gizli anahtarı oluşturabilirsiniz.
3. [İlkelerinizi oluşturma](active-directory-b2c-reference-policies.md) tooobtain ilke adları.

## <a name="samples"></a>Örnekler

* [Node.js kullanarak bir tek sayfalı uygulama oluşturma](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [.NET kullanarak bir tek sayfalı uygulama oluşturma](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

