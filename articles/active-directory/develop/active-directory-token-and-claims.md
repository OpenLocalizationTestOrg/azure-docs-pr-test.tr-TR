---
title: "Merhaba farklı belirteç ve talep türleri Azure AD tarafından desteklenen hakkında aaaLearn | Microsoft Docs"
description: "Anlama ve değerlendirme hello Taleplerde hello SAML 2.0 ve Azure Active Directory (AAD tarafından) yayınlanan JSON Web belirteçleri (JWT) belirteçleri için bir kılavuz"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Azure AD belirteç başvurusu
Azure Active Directory (Azure AD), her kimlik doğrulama akışı hello işlenmesini güvenlik belirteçlerinde çeşitli türlerde yayar. Bu belgede hello biçimi, güvenlik özellikleri ve her tür bir belirteç içeriği açıklanmaktadır.

## <a name="types-of-tokens"></a>Belirteç türleri
Azure AD destekleyen hello [OAuth 2.0 Yetkilendirme Protokolü](active-directory-protocols-oauth-code.md), hangi yapar access_tokens ve refresh_tokens kullanın.  Kimlik doğrulama ve oturum açma aracılığıyla da destekler [Openıd Connect](active-directory-protocols-openid-connect-code.md), belirteç, hello id_token üçüncü türü sunar.  Bu belirteçler her "taşıyıcı belirteç" olarak gösterilir.

Bir basit güvenlik belirteci verir "bearer" erişim tooa hello korumalı kaynak bir taşıyıcı belirtecidir. Bu anlamda hello "bearer" Merhaba belirteci sunabilir herhangi bir tarafa ' dir. Azure AD ile kimlik doğrulaması gereklidir ancak bir taşıyıcı belirteci tooreceive sipariş, istenmeyen bir taraf adımları toosecure hello belirteç, tooprevent kişiler tarafından ele alınması gerekir. Taşıyıcı belirteçlerini bunları kullanarak yerleşik mekanizması yetkisiz tooprevent tarafların olmadığı için Aktarım Katmanı Güvenliği (HTTPS) gibi güvenli bir kanal taşınan gerekir. Bir taşıyıcı belirteci hello Temizle iletilirse, ADAM bileşenini hello Orta saldırı kullanılan tooacquire hello belirteci olması ve yetkisiz erişim korumalı tooa kaynak geçirmesine. Merhaba aynı güvenlik ilkelerini depolamak veya taşıyıcı belirteçlerini daha sonra kullanmak için önbelleğe alma uygulayın. Her zaman uygulamanızı aktarır ve güvenli bir şekilde taşıyıcı belirteçleri depolar emin olun. Taşıyıcı belirteçlerini hakkında daha fazla güvenlik konuları için bkz: [RFC 6750 bölüm 5](http://tools.ietf.org/html/rfc6750).

Azure AD tarafından yayınlanan hello belirteçleri birçoğu, JSON Web belirteçlerini veya Jwt'ler olarak uygulanır.  JWT, iki taraf arasında bilgi aktarma compact, URL için güvenli bir yoludur.  Jwt'ler içinde bulunan hello bilgileri bilinir "talep" ya da bilgi onaylar hello taşıyıcı ve konu hello belirtecinin hakkında.  Jwt'ler Hello Taleplerde kodlanmış ve aktarım için seri JSON nesneleridir.  Azure AD tarafından verilen hello Jwt'ler imzalanmış, ancak şifreli olduğundan, hata ayıklama amacıyla JWT Merhaba içeriğine kolayca inceleyebilirsiniz.  Bunu aşağıdaki gibi yapmak kullanılabilen çeşitli araçlar vardır [jwt.calebb.net](http://jwt.calebb.net). Jwt'ler hakkında daha fazla bilgi için toohello başvurabilir [JWT belirtimi](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Id_tokens
Id_tokens olan bir form kimlik doğrulaması kullanarak gerçekleştirirken uygulamanızı alan oturum açma güvenlik belirtecinin [Openıd Connect](active-directory-protocols-openid-connect-code.md).  Olarak temsil [Jwt'ler](#types-of-tokens)ve uygulamanıza hello kullanıcı imzalamak için kullanabileceğiniz talepleri içerir.  Merhaba talep bir id_token kullanabileceğiniz uygun gördüğünüz - hesap bilgilerini görüntüleme veya erişim denetimi kararları bir uygulama için sık kullanılan olarak.

Id_tokens imzalanmış, ancak şu anda şifrelenmez.  Uygulamanızı bir id_token aldığında, gerekir [hello imzayı doğrulamak](#validating-tokens) tooprove belirtecin Orijinallik hello ve hello belirteci tooprove birkaç Taleplerde geçerliliğini doğrulayın.  Merhaba bir uygulama tarafından doğrulanmış talep senaryonun gereksinimlerine bağlı olarak farklılık gösterir, ancak bazı vardır [ortak talep doğrulamaları](#validating-tokens) , uygulamanızı her senaryoda gerçekleştirmeniz gerekir.

Bilgi için bölümüne id_tokens talep yanı sıra üzerinde bir örnek id_token aşağıdaki hello bakın.  İd_tokens Hello Taleplerde belirli bir sırada döndürülmez unutmayın.  Ayrıca, yeni talep id_tokens herhangi bir noktada içine zamanında tanıtılabilir - yeni talep sunulduğu şekilde uygulamanızı parçalara değil.  Merhaba aşağıdaki listede uygulamanızı güvenilir bir şekilde bu yazma hello zaman çevirebilir hello talepleri içerir.  Gerekirse, daha fazla ayrıntı hello bulunup bulunmadığını [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Örnek id_token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Uygulama için içine yapıştırarak hello örnek id_token hello Taleplerde inceleniyor deneyin [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>İd_tokens talepleri
> [!div class="mx-codeBreakAll"]
| JWT talep | Ad | Açıklama |
| --- | --- | --- |
| `appid` |Uygulama Kimliği |Merhaba belirteci tooaccess bir kaynağı kullanarak hello uygulamayı tanımlar. Merhaba uygulaması bir kullanıcı adına veya kendisi olarak davranamaz. Merhaba uygulama kimliği genellikle Uygulama nesnesini temsil eder, ancak ayrıca Azure AD içinde bir hizmet sorumlusu nesnesi gösterebilir. <br><br> **Örnek JWT değer**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Hedef kitle |Merhaba alıcı hello belirtecin amacı. Merhaba belirteç alan Merhaba uygulaması hello İzleyici değeri doğru olduğundan ve farklı bir izleyici için amaçlanan herhangi bir belirtece Reddet doğrulamanız gerekir. <br><br> **Örnek SAML değer**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Örnek JWT değer**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |Uygulama kimlik doğrulama bağlamı sınıf başvurusu |Merhaba istemcinin kimlik doğrulamasının nasıl yapıldığı gösterir. Ortak bir istemci için hello değer 0'dır. İstemci Kimliğini ve istemci gizli anahtarı kullandıysanız, başlangıç değeri 1'dir. <br><br> **Örnek JWT değer**: <br> `"appidacr": "0"` |
| `acr` |Kimlik doğrulama bağlamı sınıf başvurusu |Nasıl hello konu, karşılıklı toohello istemcisi hello uygulama kimlik doğrulama bağlamı sınıf başvurusu talep olarak doğrulanmış olduğunu gösterir. Merhaba son kullanıcı kimlik doğrulaması ISO/IEC 29115 hello gereksinimlerini karşılamayan "0" değerini gösterir. <br><br> **Örnek JWT değer**: <br> `"acr": "0"` |
| Anlık kimlik doğrulaması |Kayıtları tarih ve saat kimlik doğrulaması gerçekleştiği hello. <br><br> **Örnek SAML değer**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Kimlik Doğrulama Yöntemi |Merhaba konu hello belirtecinin nasıl doğrulandı tanımlar. <br><br> **Örnek SAML değer**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Örnek JWT değer**:`“amr”: ["pwd"]` |
| `given_name` |Ad |Merhaba, hello Azure AD kullanıcı nesnesindeki belirlenen ilk veya "verilen" Merhaba kullanıcının adını sağlar. <br><br> **Örnek SAML değer**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Örnek JWT değer**: <br> `"given_name": "Frank"` |
| `groups` |Gruplar |Merhaba ilgilinin grup üyelikleri temsil eden nesne kimlikleri sağlar. Bu değerler benzersiz (nesne kimliği bakın) ve güvenli bir şekilde yetkilendirme tooaccess kaynak zorlama gibi erişimi yönetmek için kullanılabilir. Merhaba grupları talep kümesinde bulunan hello grupları hello uygulama bildiriminin hello "groupMembershipClaims" özelliği aracılığıyla bir uygulama başına temelinde yapılandırılır. Bir null değeri tüm grupları dışlayacak, Active Directory güvenlik grubu üyeliği ve bir değer "Tümü" bırakılacak güvenlik grupları ve Office 365 dağıtım listeleri içerir yalnızca "Güvenlik grubuna" değerini içerir. <br><br> **Örnek SAML değer**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Örnek JWT değer**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Kimlik Sağlayıcısı |Merhaba belirtecinin hello konu kimliği doğrulanmış hello kimlik sağlayıcısı kaydeder. Bu değer hello verenin talep hello veren daha farklı bir kiracıdaki hello kullanıcı hesabı olmadığı sürece aynı toohello değeridir. <br><br> **Örnek SAML değer**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Örnek JWT değer**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Hangi hello belirteci verilmiş hello zaman depolar. Genellikle kullanılan toomeasure belirteci yenilik olur. <br><br> **Örnek SAML değer**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Örnek JWT değer**: <br> `"iat": 1390234181` |
| `iss` |Veren |Merhaba belirteci oluşturur ve hello güvenlik belirteci hizmeti (STS) tanımlar. Azure AD döndürür hello belirteçlerinde hello veren sts.windows.net ' dir. Merhaba hello verenin talep değeri GUID hello Kiracı hello Azure AD dizini kimliğidir. Merhaba Kiracı kimliği hello dizininin değişmez ve güvenilir bir tanımlayıcıdır. <br><br> **Örnek SAML değer**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Örnek JWT değer**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Soyadı |Merhaba son adı, Soyadı veya hello kullanıcının aile adını hello Azure AD kullanıcı nesnesinde tanımlanan sağlar. <br><br> **Örnek SAML değer**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Örnek JWT değer**: <br> `"family_name": "Miller"` |
| `unique_name` |Ad |Merhaba konu hello belirtecinin tanımlayan bir insan okunabilir değer sağlar. Bu değeri toobe Kiracı içinde benzersiz kesin değildir ve yalnızca görüntüleme amacıyla kullanılan tasarlanmış toobe. <br><br> **Örnek SAML değer**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Örnek JWT değer**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |Nesne Kimliği |Bir nesnenin benzersiz bir tanımlayıcı Azure AD'de içerir. Bu değer sabittir ve yeniden atandığında yeniden ya da silinemez. Merhaba nesne kimliği tooidentify nesneyi sorgular tooAzure AD kullanın. <br><br> **Örnek SAML değer**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Örnek JWT değer**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |Roller |Erişim denetimi konu hello tüm uygulama rolleri doğrudan ve dolaylı olarak Grup üyeliğiyle verildi ve kullanılan tooenforce rol tabanlı olabilir temsil eder. Uygulama rolleri hello aracılığıyla bir uygulama başına temelinde tanımlanan `appRoles` hello uygulama bildirimi özelliği. Merhaba `value` hello rolleri talep görünen hello değeri her uygulama rolü özelliğidir. <br><br> **Örnek SAML değer**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Örnek JWT değer**: <br> `“roles”: ["Admin", … ]` |
| `scp` |Kapsam |Merhaba kimliğe bürünme izinleri verilen toohello istemci uygulaması gösterir. Merhaba varsayılan izni `user_impersonation`. Kaynak güvenli hello Hello sahibi Azure AD içinde ek değerler kaydedebilirsiniz. <br><br> **Örnek JWT değer**: <br> `"scp": "user_impersonation"` |
| `sub` |Konu |Hangi hello hakkında hello kullanıcı bir uygulama gibi bilgileri belirteci onaylar hello asıl tanımlar. Bu değer sabittir ve atanamaz veya yeniden, bu nedenle kullanılan tooperform yetkilendirme denetimleri güvenli olabilir. Merhaba konu her zaman mevcut olduğundan hello hello Azure AD sorunları belirteçler, bu değerin bir genel amaçlı yetkilendirme sisteminde kullanılması önerilir. <br> `SubjectConfirmation`bir talep değil. Bunu hello konu hello belirtecinin nasıl doğrulanır açıklar. `Bearer`Bu hello konu hello belirteci kendi mülkü tarafından onaylanıp gösterir. <br><br> **Örnek SAML değer**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Örnek JWT değer**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |Kiracı Kimliği |Merhaba belirteç hello dizin Kiracı tanımlayan bir değişmez, yeniden kullanılabilir olmayan tanımlayıcısı. Çok kiracılı uygulamada bu değer tooaccess Kiracı özgü dizin kaynakları kullanabilir. Örneğin, bu değer tooidentify hello Kiracı bir çağrı toohello grafik API'sini kullanabilirsiniz. <br><br> **Örnek SAML değer**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Örnek JWT değer**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Belirteç ömrü |Bir belirtecin geçerli olduğu hello zaman aralığı tanımlar. Merhaba belirteci doğrular hello hizmeti bu hello hello belirteci reddetme hello belirteç ömrü içinde başka geçerli tarihidir doğrulamanız gerekir. Merhaba hizmeti için hello belirteç ömrü aralığı tooaccount ötesinde toofive dakika farklılıklarını saatin ("saat eğriltme") için yukarı Azure AD arasında izin verebilir ve hello hizmeti. <br><br> **Örnek SAML değer**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Örnek JWT değer**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Kullanıcı asıl adı |Depoları asıl hello kullanıcının kullanıcı adını hello.<br><br> **Örnek JWT değer**: <br> `"upn": frankm@contoso.com` |
| `ver` |Sürüm |Merhaba belirteci Hello sürüm numarasını depolar. <br><br> **Örnek JWT değer**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Erişim belirteçleri
Başarılı kimlik doğrulaması sırasında Azure AD kullanılan tooaccess korumalı kaynaklar olabilir bir erişim belirteci döndürür. Merhaba erişim belirteci JSON Web Token (JWT) bir base 64 kodlu ve içeriğinin bir kod çözücü çalıştırarak denetlenecek ' dir.

Varsa, uygulamanızın yalnızca *kullanır* erişim belirteçleri tooget erişim tooAPIs, erişim belirteçleri tamamen opak olarak kabul edebilirsiniz ve gereken - bunlar, uygulamanızın HTTP isteklerine tooresources ileten yalnızca dizelerdir.

Bir erişim belirteci istediğinde, Azure AD Ayrıca, uygulamanızın tüketimi için hello erişim belirtecini hakkında bazı meta verileri döndürür.  Bu bilgiler hello erişim belirteci hello kapsamlar için geçerlidir ve hello sona erme saati içerir.  Bu, uygulama tooperform akıllı tooparse hello erişim belirteci kendisini açmak zorunda kalmadan erişim belirteçleri önbelleğe almayı sağlar.

Ardından, uygulamanızın HTTP isteklerine erişim belirteçleri bekliyor Azure AD ile korunan bir API ise, doğrulama ve İnceleme aldığınız hello belirteçlerin gerçekleştirmeniz gerekir. Uygulamanızı tooaccess kaynakları kullanmadan önce hello erişim belirteci doğrulaması gerçekleştirmeniz gerekir. Doğrulama hakkında daha fazla bilgi için lütfen bkz [doğrulama belirteçleri](#validating-tokens).  
Toodo nasıl .NET ile bakın ile ilgili ayrıntılar için [Azure AD'den taşıyıcı belirteçlerini kullanarak bir Web API korumak](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Yenileme belirteçlerini

Yenileme belirteçleri olan uygulamanızı kullanabilirsiniz güvenlik belirteçleri tooacquire yeni bir OAuth 2.0 akışı belirteçleri erişim.  Bir kullanıcı adına, uygulama tooachieve uzun vadeli erişim tooresources hello kullanıcı etkileşimi gerektirmeden sağlar.

Yenileme belirteçleri çok kaynak.  Tooa tamamen farklı kaynak erişim belirteçleri için bir kaynak tarihinde için bir yenileme belirteci bir belirteç isteğini sırasında alınan toosay olmasıdır. toodo Bu, kümesi hello `resource` hello isteği toohello parametresinde hedeflenen kaynak.

Yenileme belirteçleri tamamen opak tooyour uygulama. Uzun süreli, ancak uygulamanızı bir yenileme belirteci bir süre için en son tooexpect yazılmamalıysa.  Çeşitli nedenlerle süredir herhangi bir anda yenileme belirteçleri geçersiz olabilir.  bir yenileme belirteci geçerliyse, uygulama tooknow tooattempt tooredeem yoldur yalnızca Merhaba, bir belirteç isteğini tooAzure AD belirteç uç noktası yaparak.

Yeni bir erişim belirteci için bir yenileme belirteci almak, hello belirteci yanıt olarak yeni bir yenileme belirteci alır.  Merhaba bir hello istekte kullanılan değiştirme, yeni verilen hello yenileme belirteci kaydetmeniz gerekir.  Bu, yenileme belirteçleri mümkün olduğunca uzun bir süre geçerli kalacağını garanti.

## <a name="validating-tokens"></a>Belirteçleri doğrulanıyor

İçinde sipariş toovalidate id_token veya bir access_token, uygulamanızı hem hello belirtecinin imzası ve hello talep doğrulamalıdır. Sipariş toovalidate erişim belirteçleri, uygulamanız da hello veren, hello İzleyici ve belirteç imzalama hello doğrulamalıdır. Bunlar hello Openıd bulma belgesindeki hello değerler karşı doğrulanmış toobe gerekir. Örneğin, hello Kiracı bağımsız hello belge adresindedir sürümüdür [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Azure AD Ara erişim belirteçleri doğrulamak için yerleşik özellikleri vardır ve aracılığıyla göz atabilirsiniz bizim [örnekleri](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) tercih ettiğiniz hello dilde toofind. Merhaba nasıl tooexplicitly doğrulamak bir JWT belirteci ile ilgili daha fazla bilgi için lütfen bkz [el ile JWT doğrulama örnek](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Kitaplıkları ve nasıl tooeasily ele belirteci doğrulama - Göster kod örnekleri sunuyoruz hello aşağıdaki bilgileri yalnızca işlem temel toounderstand hello istediğiniz olanlar için sağlanır.  Ayrıca çeşitli üçüncü taraf açık kaynak kitaplıkları JWT doğrulama için kullanılabilir olduğundan - neredeyse her platform ve ölçeklendiriyor dili için en az bir seçenek yoktur. Azure AD kimlik doğrulama kitaplıkları ve kod örnekleri hakkında daha fazla bilgi için lütfen bkz [Azure AD kimlik doğrulama kitaplıkları](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>Merhaba imza doğrulama

JWT'nin hello tarafından ayrılmış olan üç segmentleri içerir `.` karakter.  Hello ilk kesimini hello bilinen **üstbilgi**, ikinci hello olarak hello **gövde**ve üçüncü hello olarak hello **imza**.  Böylece, uygulamanız tarafından güvenilen hello imza segment kullanılan toovalidate hello hello belirteci özgünlüğünü olabilir.

Azure AD tarafından yayınlanan belirteçleri RSA 256 gibi endüstri standart asimetrik şifreleme algoritmaları kullanılarak imzalanmıştır. Merhaba JWT Hello üstbilgisi hello anahtarı hakkında bilgi içerir ve toosign hello belirteç şifreleme yöntemi kullanılır:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Merhaba `alg` talep gösterir hello sırasında kullanılan toosign hello belirteci olan hello algoritması `x5t` talep kullanılan toosign hello belirteci olan hello belirli ortak anahtarı gösterir.

Herhangi bir anda zaman, belirli bir genel-özel anahtar çiftleri kümesini herhangi birini kullanarak bir id_token Azure AD oturum. Uygulamanız bu anahtarı otomatik olarak değiştirir toohandle yazılması gereken şekilde azure AD hello olası anahtarları düzenli aralıklarla kümesini döndürür.  Azure AD tarafından kullanılan güncelleştirmeleri toohello ortak anahtarları için makul sıklığı toocheck her 24 saattir.

Meta veri belgesi Openıd Connect hello konumunda bulunan kullanarak anahtar veri gerekli toovalidate hello imzası imzalama hello elde edebilirsiniz:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Bu URL'yi bir tarayıcıda deneyin!
> 
> 

Bu meta veri belgesi, çeşitli uç noktaları Openıd Connect kimlik doğrulama gerçekleştirmek için gereken hello hello konumunu gibi bilgiler çeşitli yararlı parçalarını içeren bir JSON nesnesidir.  

Ayrıca içeren bir `jwks_uri`, toosign belirteçleri kullanılan ortak anahtarlar hello kümesi hello konumunu sağlayan.  Merhaba JSON belgesi hello bulunan `jwks_uri` tüm zaman içinde belirli o anda kullanımda hello ortak anahtar bilgileri içerir.  Uygulamanızı hello kullanabilirsiniz `kid` hello JWT üstbilgi tooselect hangi ortak anahtar bu belgede kullanılan toosign açıldı belirli bir belirteç talep.  Ardından, imza doğrulaması hello doğru ortak anahtar ve hello belirtilen algoritmasını kullanarak gerçekleştirebilirsiniz.

İmza doğrulaması gerçekleştirme, bu belgenin dış hello kapsamı - birçok açık kaynak kitaplıkları, gerekirse, bunu yardımcı olduğunuz için kullanılabilir.

#### <a name="validating-hello-claims"></a>Merhaba talep doğrulama

Uygulamanızı bir belirteç (kullanıcı oturum açma sırasında bir id_token ya da bir erişim belirteci hello HTTP isteği bir taşıyıcı belirteci olarak) aldığında, birkaç denetimleri hello talep karşı hello belirteçte gerçekleştirmelisiniz.  Bunlar dahil ancak bunlarla sınırlı değildir:

* Merhaba **İzleyici** talep - belirteç hello tooverify tooyour uygulama verilen hedeflenen toobe oluştu.
* Merhaba **önce değil** ve **süre sonu** talep - token hello tooverify değil süresi doldu.
* Merhaba **veren** talep - token hello tooverify tooyour uygulama gerçekten Azure AD tarafından yayınlandı.
* Merhaba **Nonce** -toomitigate belirteç yeniden yürütme saldırısını.
* ve daha fazlası...

Uygulamanız için kimlik belirteçlerini gerçekleştirmesi gerektiğini talep doğrulamaları tam bir listesi için toohello bakın [Openıd Connect belirtimi](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). Bu talep için hello beklenen değerler ayrıntılarını hello önceki dahil [id_token bölüm](#id-tokens) bölümü.

## <a name="sample-tokens"></a>Örnek belirteçleri

Bu bölümde Azure AD döndürür SAML ve JWT belirteçleri örneklerini görüntüler. Bu örnekleri hello talep bağlamda görmenize olanak tanır.

### <a name="saml-token"></a>SAML belirteci

Bu, tipik bir SAML belirtecine örneğidir.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>JWT belirteci - kullanıcı kimliğine bürünme
Bir yetkilendirme kodu verme akışında kullanılan bir tipik JSON web token (JWT) örneğidir.
Toplama tooclaims içinde hello belirteci bir sürüm numarası içeren **ver** ve **appidacr**, hello istemcinin kimlik doğrulamasının nasıl yapıldığı gösteren hello kimlik doğrulama bağlamı sınıf başvurusu,. Ortak bir istemci için hello değer 0'dır. Bir istemci kimliği veya istemci gizli kullanıldıysa, başlangıç değeri 1'dir.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>İlgili içerik
* Hello Azure AD grafik bkz [İlkesi işlemleri](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) ve hello [İlkesi varlık](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn belirteç ömrü ilkesi hello Azure AD grafik API'si aracılığıyla yönetme hakkında daha fazla bilgi.
* Daha fazla bilgi ve örnekler dahil olmak üzere, PowerShell cmdlet'leri aracılığıyla ilkelerini yönetme örnekleri için bkz: [yapılandırılabilir belirteci yaşam süreleri Azure AD'de](../active-directory-configurable-token-lifetimes.md). 
