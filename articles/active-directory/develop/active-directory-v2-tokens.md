---
title: "aaaAzure Active Directory v2.0 belirteçler başvurusu | Microsoft Docs"
description: "hello Azure AD v2.0 uç tarafından gösterilen talep ve belirteç Hello türleri"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Azure Active Directory v2.0 belirteç başvurusu
Hello Azure Active Directory (Azure AD) v2.0 uç yayar her güvenlik belirteçleri çeşitli türlerde [kimlik doğrulaması akışı](active-directory-v2-flows.md). Bu başvuru hello biçimi, güvenlik özellikleri ve her tür belirteç içeriğini açıklar.

> [!NOTE]
> Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez. mı hello v2.0 uç kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>
>

## <a name="types-of-tokens"></a>Belirteç türleri
Merhaba v2.0 uç destekleyen hello [OAuth 2.0 yetkilendirme protokolünü](active-directory-v2-protocols.md), kullanan erişim belirteçleri ve yenileme belirteçleri. Merhaba v2.0 uç de destekleyen kimlik doğrulama ve oturum açma aracılığıyla [Openıd Connect](active-directory-v2-protocols.md). Openıd Connect, hello kimliği token üçüncü türü sunar. Bu belirteçler her olarak temsil edilen bir *taşıyıcı* belirteci.

Bir basit güvenlik belirteci verir taşıyıcı erişim tooa hello korumalı kaynak bir taşıyıcı belirtecidir. Merhaba taşıyıcı hello belirteci sunabilir herhangi bir tarafa ' dir. Adımları toosecure hello belirteci iletim ve depolama sırasında katılmaz varsa bir taraf Azure AD tooreceive hello taşıyıcı belirteci ile kimlik doğrulaması yapmalıdır olsa da ele ve istenmeyen bir şahıs tarafından kullanılır. Bazı güvenlik belirteçleri bunları ancak taşıyıcı belirteçleri kullanmayan gelen yerleşik mekanizması yetkisiz tooprevent tarafların vardır. Aktarım Katmanı Güvenliği (HTTPS) gibi güvenli bir kanal taşıyıcı belirteçlerini taşınan gerekir. Bu tür güvenlik bir taşıyıcı belirteci iletilirse, kötü amaçlı bir taraf "man-in--middle saldırı" tooacquire hello belirteci kullanın ve yetkisiz erişim korumalı tooa kaynak için kullanın. Merhaba aynı güvenlik ilkelerini depolamak veya taşıyıcı belirteçlerini daha sonra kullanmak için önbelleğe alma uygulayın. Uygulamanızı güvenli bir şekilde iletir ve taşıyıcı belirteçleri depolar her zaman emin olun. Taşıyıcı belirteçler için daha fazla güvenlik konuları için bkz: [RFC 6750 bölüm 5](http://tools.ietf.org/html/rfc6750).

Merhaba v2.0 uç noktası tarafından yayınlanan hello belirteçleri çoğunu JSON Web belirteçleri (Jwt'ler) uygulanır. JWT, iki taraf arasında compact, URL için güvenli şekilde tootransfer bilgilerdir. JWT'nin Hello bilgilerinde adlı bir *talep*. Bu bir onaylama hello taşıyıcı hakkındaki bilgileri ve konu hello belirtecinin olur. JWT'nin Hello Taleplerde kodlanmış ve aktarım için seri hale getirilmiş JavaScript nesne gösterimi (JSON) nesneleridir. Merhaba Jwt'ler tarafından verilen çünkü hello v2.0 uç imzalanmış ancak şifreli, hata ayıklama amacıyla kolayca JWT Merhaba içeriğine inceleyebilirsiniz. Merhaba Jwt'ler hakkında daha fazla bilgi için bkz: [JWT belirtimi](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Kimliği belirteçleri
Bir kimliği belirteci kullanarak kimlik doğrulaması gerçekleştirdiğinde, uygulamanızı alan oturum açma güvenlik belirteci biçimidir [Openıd Connect](active-directory-v2-protocols.md). Kimlik belirteçlerini olarak temsil [Jwt'ler](#types-of-tokens), tooyour uygulamada toosign hello kullanıcı kullanabilir talepleri içerir. Merhaba talep kimliği belirteci çeşitli şekillerde kullanabilirsiniz. Genellikle, Yöneticiler bir uygulamada kimliği belirteçleri toodisplay hesap bilgileri veya toomake erişim denetimi kararlarını kullanın. Merhaba v2.0 uç tutarlı bir oturum kullanıcı hello türünü bağımsız olarak talepler kümesi sahip kimliği belirteci yalnızca bir tür yayınlar. Merhaba biçimini ve kimlik belirteçlerini içeriğini olan hello aynı iş veya Okul hesapları ve kişisel Microsoft hesabı kullanıcıları için.

Şu anda kimlik belirteçlerini imzalanmış fakat şifrelenmez. Uygulamanızı bir kimliği belirteci aldığında, gerekir [hello imzayı doğrulamak](#validating-tokens) tooprove belirtecin Orijinallik hello ve hello belirteci tooprove birkaç Taleplerde geçerliliğini doğrulayın. Merhaba bir uygulama tarafından doğrulanmış talep senaryonun gereksinimlerine bağlı olarak farklılık gösterir, ancak uygulamanızı bazı gerçekleştirmelisiniz [ortak talep doğrulamaları](#validating-tokens) her senaryoda.

Biz size kimliği belirteçleri Taleplerde ilgili tam Ayrıntılar hello hello bölümlerde, ayrıca tooa örnek kimliği belirteci. Talep Kimliği belirteçlerinde belirli bir sırada döndürülmez unutmayın. Ayrıca, yeni talep kimliği belirteçlere herhangi bir zamanda tanıtılabilir. Yeni Talep sunulduğunda, uygulamanızın çalışmamasına neden değil. liste aşağıdaki hello uygulamanız şu anda güvenilir bir şekilde çevirebilir hello talepleri içerir. Hello daha fazla ayrıntı bulabilirsiniz [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-id-token"></a>Örnek kimliği belirteci
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> Uygulama için tooinspect hello hello örnek kimliği belirteçte talep yapıştırın hello örnek kimliği belirtece [calebb.net](http://calebb.net/).
>
>

#### <a name="claims-in-id-tokens"></a>Talep Kimliği belirteçlerinde
| Ad | İste | Örnek değer | Açıklama |
| --- | --- | --- | --- |
| Hedef kitle |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Merhaba hedeflenen alıcı hello belirtecinin tanımlar. Kimliği belirteçlerinde hello İzleyici uygulamanızın uygulama hello Microsoft uygulama kayıt portalı tooyour uygulamada atanan kimliğidir. Uygulamanız bu değeri doğrulamak ve hello değeri eşleşmiyorsa hello belirteci reddetme gerekir. |
| Veren |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Oluşturur ve hello belirtecini ve hangi hello kullanıcı kimlik doğrulamasının yapıldığı hello Azure AD kiracısı döndüren hello güvenlik belirteci hizmeti (STS) tanımlar. Uygulamanızı hello verenin talep belirteci hello tooensure hello v2.0 uç noktasından gelen doğrulamalıdır. Ayrıca hello GUID hello talep toorestrict hello toohello uygulamada oturum kiracılar kümesi bölümünü kullanmanız gerekir. Merhaba hello kullanıcı gösteren bir Microsoft hesabı tüketici kullanıcıdan GUID'dir `9188040d-6c67-4c5b-b112-36a304b66dad`. |
| çıkışı |`iat` |`1452285331` |hello zaman hangi hello belirteci, dönem saatle gösterilir verilmiş. |
| süre sonu |`exp` |`1452289231` |hangi hello belirteci geçersiz olduğu hello zaman dönem zamanında temsil. Uygulamanızı hello belirteç ömrü bu talep tooverify hello geçerliliğini kullanmanız gerekir. |
| önce değil |`nbf` |`1452285331` |Dönem zamanında temsil hello zaman hangi hello belirteç geçerli olur. Bu, genellikle aynı hello verme sürede hello olur. Uygulamanızı hello belirteç ömrü bu talep tooverify hello geçerliliğini kullanmanız gerekir. |
| Sürüm |`ver` |`2.0` |Azure AD tarafından tanımlandığı şekilde hello kimliği belirteci Hello sürümü. Merhaba v2.0 uç noktası için hello değerdir `2.0`. |
| Kiracı kimliği |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |Kullanıcı hello hello Azure AD Kiracı temsil eden bir GUID değil. İş ve Okul hesapları için hello GUID hello değişmez Kiracı Kullanıcı hello hello kuruluşun Kimliğini ait olur. Kişisel hesaplar için hello değerdir `9188040d-6c67-4c5b-b112-36a304b66dad`. Merhaba `profile` kapsam gereklidir, bu talep tooreceive sipariş. |
| kod karma |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |yalnızca bir OAuth 2.0 yetkilendirme koduyla hello kimliği belirteci verildiğinde hello kod karma kimlik belirteçlerini dahil edilir. Bir yetkilendirme kodu kullanılan toovalidate hello özgünlüğünü olabilir. Bu doğrulama gerçekleştirme hakkında daha fazla bilgi için bkz: hello [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html). |
| erişim belirteci karma |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |yalnızca bir OAuth 2.0 erişim belirteciyle hello kimliği belirteci verildiğinde hello erişim belirteci karma kimlik belirteçlerini dahil edilir. Bir erişim belirteci kullanılan toovalidate hello özgünlüğünü olabilir. Bu doğrulama gerçekleştirme hakkında daha fazla bilgi için bkz: hello [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html). |
| nonce |`nonce` |`12345` |Merhaba nonce belirteç yeniden yürütme saldırılarını Azaltıcı stratejidir. Uygulamanızı bir nonce bir yetkilendirme isteği hello kullanarak belirtebilirsiniz `nonce` sorgu parametresi. Merhaba istekte sağladığınız hello değeri hello kimliği belirtecin içinde gösterilen `nonce` değiştirilmemiş talep. Uygulamanızı belirli bir kimliği belirteciyle hello uygulamanın oturum ilişkilendirir hello isteğinde belirtilen hello değeri karşı hello değer doğrulayabilirsiniz. Uygulamanızı hello kimliği belirteci doğrulama işlemi sırasında bu doğrulama gerçekleştirmeniz gerekir. |
| ad |`name` |`Babe Ruth` |Merhaba adı talebi hello konu hello belirtecinin tanımlayan okunabilir bir değer sağlar. Merhaba değeri yalnızca görüntüleme amacıyla kullanılan toobe toobe değişebilir olduğundan ve onu benzersiz tasarlanmış garanti edilmez. Merhaba `profile` kapsam gereklidir, bu talep tooreceive sipariş. |
| E-posta |`email` |`thegreatbambino@nyy.onmicrosoft.com` |Merhaba birincil e-posta adresi varsa, hello kullanıcı hesabıyla ilişkilendirilmiş. Değerini değişebilir ve zaman içinde değişebilir. Merhaba `email` kapsam gereklidir, bu talep tooreceive sipariş. |
| tercih edilen kullanıcı adı |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |Merhaba v2.0 uç hello kullanıcı temsil eden hello birincil kullanıcı adı. Bir e-posta adresi, telefon numarası ya da belirtilen biçim olmadan genel bir kullanıcı adı olabilir. Değerini değişebilir ve zaman içinde değişebilir. Merhaba `profile` kapsam gereklidir, bu talep tooreceive sipariş. |
| Konu |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | Merhaba, belirteç hello hakkında asıl hello kullanıcı, bir uygulamanın gibi bilgileri onaylar. Bu değer sabittir ve yeniden atandığında yeniden ya da silinemez. Bu kullanılan tooperform yetkilendirme denetimleri güvenli bir şekilde, ne zaman hello belirteci kullanılan tooaccess bir kaynaktır ve gibi veritabanı tablolarındaki anahtar olarak kullanılan olabilir. Merhaba konu her zaman hello belirteçleri mevcut olduğundan bu Azure AD verir, bu değer bir genel amaçlı yetkilendirme sisteminde kullanmanızı öneririz. Merhaba konu, ancak, ikili bir tanımlayıcıdır. - benzersiz tooa belirli uygulama kimliğidir.  Bu nedenle, iki farklı istemci kimliği kullanarak iki farklı uygulamalarda tek bir kullanıcı oturum açtığında, bu uygulamaları hello konu talep için iki farklı değerler alır.  Bu olabilir veya mimarisi ve gizlilik gereksinimlerinize bağlı olarak gerekli değildir. |
| Nesne Kimliği |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | bir nesne için değişmez tanımlayıcı hello Microsoft Identity sistemde, bu durumda, bir kullanıcı hesabı hello.  Güvenli ve anahtar veritabanı tabloları olarak kullanılan tooperform yetkilendirme denetimleri de olabilir. Bu kimliği hello kullanıcı uygulamalar arasında benzersiz şekilde tanımlar.-aynı kullanıcının alacağı hello imzalama iki farklı uygulamalar aynı hello hello değerinde `oid` talep.  Başka bir deyişle, bu sorguları hello Microsoft Graph gibi tooMicrosoft Çevrimiçi Hizmetler yaparken kullanılabilir.  Merhaba Microsoft Graph, bu kimliği hello olarak döndürecektir `id` özelliği için belirtilen kullanıcı hesabı.  Çünkü hello `oid` birden fazla uygulama toocorrelate, hello kullanıcılara `profile` kapsam gereklidir, bu talep tooreceive sipariş. Tek bir kullanıcı birden fazla kiracılar varsa, her bir kiracı farklı nesne Kimliğinde hello kullanıcı içerecek Not - aynı kimlik bilgilerini hello kullanıcının her hesabıyla oturum açtığı hello olsa bile farklı hesaplar kabul edilir. |

### <a name="access-tokens"></a>Erişim belirteçleri
Şu anda hello v2.0 uç noktası tarafından verilen erişim belirteçleri, yalnızca Microsoft Services tarafından kullanılabilecek. Uygulamalarınızı tooperform herhangi bir doğrulama veya denetleme erişim belirteçlerinin senaryoların herhangi biri şu anda desteklenen hello için gereken döndürmemelidir. Erişim belirteci olarak tamamen opak davranabilirsiniz. Bunlar, uygulamanızın HTTP isteklerine tooMicrosoft geçirebilirsiniz yalnızca dizelerdir.

Gelecekteki hello v2.0 yakın hello içinde bitiş noktası diğer istemcilerinden hello özelliği, uygulama tooreceive erişim belirteçleri için tanıtılacaktır. O anda hello bu konudaki bilgiler, başvuru, uygulama tooperform erişim belirteci doğrulama ve benzer diğer görevler için gereksinim duyduğunuz hello bilgilerle güncelleştirilir.

Bir erişim belirteci hello v2.0 uç noktasından istediğinde hello v2.0 uç Ayrıca, uygulama toouse için hello erişim belirtecini hakkındaki meta verileri döndürür. Bu bilgiler hello erişim belirteci hello kapsamlar için geçerlidir ve hello sona erme saati içerir. Bu meta verileri tooperform akıllı erişim belirteçleri tooparse açık hello erişim belirteci kendisini gerek kalmadan önbelleğe alma, uygulamanızın kullanır.

### <a name="refresh-tokens"></a>Yenileme belirteçlerini
Yenileme belirteçlerini uygulamanızı tooget yeni kullanabilirsiniz güvenlik belirteçleri erişim belirteçleri bir OAuth 2.0 akışı şunlardır. Uygulamanız, bir kullanıcı adına hello kullanıcı ile etkileşimi gerektirmeden yenileme belirteçleri tooachieve uzun vadeli erişim tooresources kullanabilirsiniz.

Yenileme belirteçleri çok kaynak. Bir kaynak için bir belirteç isteğini sırasında alınan bir yenileme belirteci erişim belirteçleri tooa tamamen farklı bir kaynak için kullanılan.

bir yenileme belirteci yanıt tooreceive, uygulamanızı istemelisiniz ve hello verilmesi `offline_acesss` kapsam. toolearn hello hakkında daha fazla `offline_access` hello bkz kapsam [onay ve kapsamları](active-directory-v2-scopes.md) makale.

Yenileme belirteçlerini olan ve her zaman olacaktır, tamamen opak tooyour uygulama. Bunlar hello Azure AD v2.0 uç tarafından verilir ve yalnızca Denetlenmekte ve hello v2.0 uç noktası tarafından yorumlanır. Uzun süreli, ancak uygulamanızı bir yenileme belirteci bir süre için en son tooexpect yazılmamalıysa. Çeşitli nedenlerle herhangi bir anda yenileme belirteçleri geçersiz olabilir. bir yenileme belirteci geçerliyse, uygulama tooknow tooattempt tooredeem yoldur yalnızca Merhaba, belirteç isteği toohello v2.0 uç noktası yaparak.

Yeni bir erişim belirteci için bir yenileme belirteci almak zaman (ve uygulamanızı hello yeterliyse `offline_access` kapsam), hello belirteci yanıt olarak yeni bir yenileme belirteci alma. Yeni verilen hello yenileme belirteci, tooreplace hello bir kullandığınız hello istekte kaydedin. Bu, yenileme belirteçleri mümkün olduğunca uzun bir süre geçerli kalacağını güvence altına alır.

## <a name="validating-tokens"></a>Belirteçleri doğrulanıyor
Şu anda yalnızca uygulamalarınızı gereksinim belirteci doğrulama hello tooperform kimlik belirteçlerini doğrulanıyor. toovalidate kimliği belirteci, uygulamanızı hello kimliği belirteci hem hello kimliği belirtecin imza ve hello talepleri doğrulamalıdır.

<!-- TODO: Link -->
Microsoft, kitaplıklar ve nasıl tooeasily ele belirteci doğrulama Göster kod örnekleri sağlar. Merhaba sonraki bölümlerde, temel alınan işlem hello açıklanmaktadır. Bazı üçüncü taraf açık kaynak kitaplıkları da JWT doğrulama için kullanılabilir. Neredeyse her platform ve dil için en az bir kitaplığın seçeneği yoktur.

### <a name="validate-hello-signature"></a>Merhaba imza doğrulama
JWT'nin hello tarafından ayrılmış olan üç segmentleri içerir `.` karakter. Merhaba ilk kesimini hello bilinen *üstbilgi*, hello ikinci kesimi ise hello *gövde*, ve hello üçüncü segment hello *imza*. Böylece, uygulamanız tarafından güvenilen hello imza segment kullanılan toovalidate hello hello kimliği belirteci özgünlüğünü olabilir.

Kimlik belirteçlerini RSA 256 gibi endüstri standardı asimetrik şifreleme algoritmaları kullanılarak imzalanmıştır. Merhaba hello kimliği belirteci üstbilgisi sahiptir hello anahtarı hakkında bilgi ve toosign hello belirteç şifreleme yöntemi kullanılır. Örneğin:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Merhaba `alg` talep kullanılan toosign hello belirteci olan hello algoritmasını belirtir. Merhaba `kid` talep kullanılan toosign hello belirteci olan hello ortak anahtarı gösterir.

Herhangi bir zamanda hello v2.0 uç belirli bir genel-özel anahtar çiftleri kümesini herhangi birini kullanarak bir kimliği belirteci oturum. Uygulamanız bu anahtarı otomatik olarak değiştirir toohandle yazılması gereken şekilde hello v2.0 uç düzenli aralıklarla hello olası anahtarlarını kümesini döndürür. Merhaba v2.0 uç noktası tarafından kullanılan güncelleştirmeleri toohello ortak anahtarları için makul sıklığı toocheck her 24 saattir.

Meta veri belgesi Openıd Connect hello konumunda bulunan kullanarak toovalidate hello imza gereksinim anahtar verilerini imzalama hello elde edebilirsiniz:

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> Merhaba URL'yi bir tarayıcıda deneyin!
>
>

Bu meta veri belgesi gibi çeşitli uç noktaları Openıd Connect kimlik doğrulaması için gerekli hello hello konumu bilgileri, çeşitli yararlı parçalarını sahip bir JSON nesnesidir.  Merhaba belge de içeren bir *jwks_uri*, toosign belirteçleri kullanılan ortak anahtarlar hello kümesi hello konumunu sağlayan. Merhaba jwks_uri bulunan hello JSON belgesi şu anda kullanımda olan tüm hello ortak anahtar bilgileri yok. Uygulamanızı hello kullanabilirsiniz `kid` hello JWT üstbilgi tooselect hangi ortak anahtar bu belgede kullanılan toosign süredir içinde bir belirteç talep. Ardından, imza doğrulaması'nin hello doğru ortak anahtar ve hello belirtilen algoritmasını kullanarak gerçekleştirir.

İmza doğrulaması gerçekleştirme, bu belgenin dış hello kapsamı değil. Birçok açık kaynak kitaplıkları kullanılabilir toohelp olduğundan, bu.

### <a name="validate-hello-claims"></a>Merhaba talep doğrula
Uygulamanızı bir kimliği belirteci kullanıcı oturum açma sırasında aldığında, bunu hello talep karşı birkaç denetimleri hello kimliği belirteçte gerçekleştirmelisiniz. Bunlar dahil ancak bunlarla sınırlı değildir:

* **Hedef kitle** talep kimliği belirteci hello tooverify tooyour uygulama verilen hedeflenen toobe edildi
* **önce değil** ve **süre sonu** talep kimliği belirteci hello tooverify süresi sona
* **veren** talep belirteci hello tooverify hello v2.0 uç noktası tarafından tooyour uygulama yayımlandığında
* **nonce**, bir belirteç yeniden yürütme saldırı azaltma

Merhaba, uygulamanızın gerçekleştirmesi gereken talep doğrulamaları tam bir listesi için bkz [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).

Bu talep için hello beklenen değerler ayrıntılarını hello dahil [kimlik belirteçlerini](# ID tokens) bölümü.

## <a name="token-lifetimes"></a>Belirteç yaşam süresi
Belirteç yaşam süreleri bilgilerinizi yalnızca aşağıdaki hello sunuyoruz. Merhaba bilgiler geliştirmek ve uygulama hata ayıklama yardımcı olabilir. Uygulamalarınızı olmamalıdır tooexpect bu yaşam süreleri tooremain sabiti hiçbirini yazılır. Yaşam süresi can belirteci ve herhangi bir zamanda değiştirir.

| Belirteç | Yaşam süresi | Açıklama |
| --- | --- | --- |
| Kimlik belirteçlerini (iş veya Okul hesapları) |1 saat |Kimlik belirteçlerini, genellikle 1 saat boyunca geçerlidir. Web uygulamanız kendi oturumunda (önerilen) hello kullanıcıyla veya tamamen farklı oturum yaşam süresi seçebilirsiniz bu aynı yaşam süresi toomaintain kullanabilirsiniz. Uygulamanızı tooget yeni bir kimliği belirteci gerekirse, toomake bir yeni oturum açma isteği toohello v2.0 uç noktası yetkilendirilmesi gerekir. Geçerli tarayıcı oturumu hello v2.0 uç noktası ile Merhaba kullanıcı varsa, hello kullanıcı değiştirilemeyebilir gerekli tooenter kimlik bilgilerini yeniden olabilir. |
| Kimlik belirteçlerini (Kişisel hesapları) |24 saat |Kişisel hesaplar için kimlik belirteçlerini, genellikle 24 saat boyunca geçerlidir. Web uygulamanız kendi oturumunda (önerilen) hello kullanıcıyla veya tamamen farklı oturum yaşam süresi seçebilirsiniz bu aynı yaşam süresi toomaintain kullanabilirsiniz. Uygulamanızı tooget yeni bir kimliği belirteci gerekirse, toomake bir yeni oturum açma isteği toohello v2.0 uç noktası yetkilendirilmesi gerekir. Geçerli tarayıcı oturumu hello v2.0 uç noktası ile Merhaba kullanıcı varsa, hello kullanıcı değiştirilemeyebilir gerekli tooenter kimlik bilgilerini yeniden olabilir. |
| Erişim belirteçleri (iş veya Okul hesapları) |1 saat |Belirteç yanıtları hello belirteci meta verilerinin bir parçası belirtilir. |
| Erişim belirteçleri (Kişisel hesapları) |1 saat |Belirteç yanıtları hello belirteci meta verilerinin bir parçası belirtilir. Kişisel hesapları adına verilen erişim belirteçleri için farklı bir yaşam süresi yapılandırılabilir, ancak 1 saat normaldir. |
| Yenileme belirteçlerini (iş veya Okul hesabı) |Too14 günleri |Bir tek yenileme belirteci 14 gün sayısı için geçerli değil. Ancak, hello yenileme belirteci başarısız kadar uygulamanızın tootry toouse bir yenileme belirteci devam şekilde ya da isteğe bağlı olarak, uygulamanızın yeni bir yenileme belirteciyle değiştirir kadar çeşitli nedenlerle herhangi bir zamanda geçersiz hale gelebilir. Bir yenileme belirteci ayrıca hello kullanıcının kimlik bilgilerini girdiği bu yana 90 gün olması durumunda geçersiz hale gelir. |
| Yenileme belirteçlerini (Kişisel hesapları) |Too1 yılı |Bir tek yenileme belirteci en fazla 1 yıl için geçerlidir. Ancak, çeşitli nedenlerle herhangi bir zamanda hello yenileme belirteci geçersiz olabilir, böylece uygulamanız tootry toouse devam bir yenileme belirteci bu kadar başarısız olur. |
| Yetkilendirme kodları (iş veya Okul hesapları) |10 dakika |Yetkilendirme kodları bilerek kısa süreli ve hello belirteçleri alındığında hemen erişim belirteçleri ve yenileme belirteçleri için kullanılan. |
| Yetkilendirme kodları (Kişisel hesapları) |5 dakika |Yetkilendirme kodları bilerek kısa süreli ve hello belirteçleri alındığında hemen erişim belirteçleri ve yenileme belirteçleri için kullanılan. Kişisel hesapları adına verilen yetkilendirme kodları tek seferlik kullanım içindir. |
