---
title: "Azure AD v2.0 tarafından desteklenen hello yetkilendirme protokolleri hakkında aaaLearn | Microsoft Docs"
description: "Hello Azure AD v2.0 uç tarafından desteklenen bir kılavuzu tooprotocols."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# v2.0 protokolleri - OAuth 2.0 & Openıd Connect
Merhaba v2.0 uç noktası kimlik olarak-hizmet endüstri standardı protokolleri, Openıd Connect ve OAuth 2.0 ile Azure AD kullanabilirsiniz.  Merhaba hizmet standartlara uygun olsa da, iki belirtilmesinden Bu protokoller arasındaki küçük farklılıklar olabilir.  Buraya Hello bilgileri doğrudan göndererek kodunuzu seçtiğiniz toowrite & işleme HTTP isteklerini veya kullanımı bir 3. taraf açma bizim açık kaynak kitaplıkları birini kullanmak yerine Kaynak Kitaplığı yararlı olacaktır.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>
>

## Merhaba temelleri
Neredeyse tüm OAuth ve Openıd Connect akışlarında, hello Exchange'de ilgili dört tarafların vardır:

![OAuth 2.0 rolleri](../../media/active-directory-v2-flows/protocols_roles.png)

* Merhaba **yetkilendirme sunucusu** hello v2.0 uç noktası.  Merhaba kullanıcının kimliğini sağlayarak, verme ve erişim tooresources iptal etme ve belirteç için sorumlu değildir.  Merhaba kimlik sağlayıcısı olarak da bilinen olduğu -, güvenli bir şekilde her şeyi işleme toodo hello kullanıcının bilgileri, kullanıcıların erişim ve hello güven ilişkileri bir akışı taraflar arasında.
* Merhaba **kaynak sahibi** hello son kullanıcı, normal olur.  Bu, hello verilerin sahibi ve hello güç tooallow olan hello taraf üçüncü o veri ya da kaynak tooaccess taraflarla olur.
* Merhaba **OAuth istemcisi** kendi uygulama kimliği ile tanımlanan uygulamanızın  Genellikle, hello son kullanıcı ile etkileşime giren ve belirteçleri hello yetkilendirme sunucusundan ister hello taraf olur.  Merhaba istemci kaynak izni tooaccess hello hello kaynak sahibi tarafından verilmiş olması gerekir.
* Merhaba **kaynak sunucusu** hello kaynak veya veri bulunduğu değil.  Merhaba yetkilendirme toosecurely kimlik doğrulaması ve hello OAuth istemci yetkilendirme sunucusu güvenir ve tooa kaynağa erişim access_tokens tooensure verilebilir taşıyıcı kullanır.

## Uygulama kaydı
Merhaba v2.0 uç noktası kullanan her uygulamanın kayıtlı toobe gerekir [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) OAuth veya Openıd Connect kullanarak etkileşim kurabilen önce.  Merhaba uygulama kayıt işlemi Topla & birkaç değerleri tooyour uygulama atayın:

* Bir **uygulama kimliği** uygulamanızı benzersiz olarak tanımlayan
* A **yeniden yönlendirme URI'si** veya **paket tanımlayıcı** kullanılan toodirect yanıtları geri tooyour app olabilir
* Diğer birkaç senaryoya özel değerler.

Daha fazla ayrıntı için nasıl çok öğrenin[uygulama kaydetmeyi](active-directory-v2-app-registration.md).

## Uç Noktalar
Kayıttan sonra hello uygulama isteklerini toohello v2.0 uç göndererek Azure AD ile iletişim kurar:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Burada hello `{tenant}` dört farklı değerler birini alabilir:

| Değer | Açıklama |
| --- | --- |
| `common` |Kişisel Microsoft hesapları ve Azure Active Directory toosign iş/Okul hesapları olan kullanıcıların hello uygulamasına sağlar. |
| `organizations` |Yalnızca Azure Active Directory toosign iş/Okul hesapları olan kullanıcıların hello uygulamasına sağlar. |
| `consumers` |Yalnızca kişisel Microsoft hesaplarını (MSA) toosign kullanıcılarla hello uygulamasına sağlar. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` veya `contoso.onmicrosoft.com` |Yalnızca belirli bir Azure Active Directory Kiracı toosign iş/Okul hesapları olan kullanıcıların hello uygulamasına sağlar.  Merhaba kolay etki alanı adını Azure AD kiracısı hello ya da hello kiracının GUID tanımlayıcısı kullanılabilir. |

Hakkında daha fazla bilgi için bu uç noktalar ile toointeract aşağıda belirli uygulama türü seçin.

## Belirteçler
Merhaba v2.0 uyarlamasını OAuth 2.0 ve Openıd Connect taşıyıcı belirteçler, taşıyıcı belirteçlerini Jwt'ler temsil dahil olmak üzere kapsamlı kullanımını olun. Bir basit güvenlik belirteci verir "bearer" erişim tooa hello korumalı kaynak bir taşıyıcı belirtecidir. Bu anlamda hello "bearer" Merhaba belirteci sunabilir herhangi bir tarafa ' dir. Merhaba adımları toosecure hello belirteçte iletim ve depolama katılmaz gerekirse bir taraf ilk Azure AD tooreceive hello taşıyıcı belirteci ile kimlik doğrulaması yapması gereken ancak ele ve istenmeyen bir şahıs tarafından kullanılır. Bazı güvenlik belirteçleri kullanarak gelen yetkisiz tarafların engellemek için yerleşik bir mekanizma olmakla birlikte, taşıyıcı belirteçlerini bu düzenek yoksa ve Aktarım Katmanı Güvenliği (HTTPS) gibi güvenli bir kanal taşınan gerekir. Bir taşıyıcı belirteci hello Temizle iletilirse, ADAM bileşenini hello Orta saldırı kötü amaçlı taraf tooacquire hello belirteci kullanılabilir ve yetkisiz erişim korumalı tooa kaynak için kullanın. Merhaba aynı güvenlik ilkelerini depolamak veya taşıyıcı belirteçlerini daha sonra kullanmak için önbelleğe alma uygulayın. Her zaman uygulamanızı aktarır ve güvenli bir şekilde taşıyıcı belirteçleri depolar emin olun. Taşıyıcı belirteçlerini hakkında daha fazla güvenlik konuları için bkz: [RFC 6750 bölüm 5](http://tools.ietf.org/html/rfc6750).

Merhaba v2.0 uç kullanılan belirteçleri farklı türdeki daha ayrıntılı bilgi sağlanmıştır [hello v2.0 uç noktası belirteç başvurusu](active-directory-v2-tokens.md).

## Protokoller
Bazı örnek istekleri, kullanmaya başlama öğreticileri aşağıda hello birini hazır toosee olup olmadığınızı.  Her biri tooa belirli kimlik doğrulama senaryosu karşılık gelir.  Sizin için doğru akış hello olduğu saptarken yardıma gerek duyarsanız kullanıma [hello hello v2.0 oluşturabilir uygulama türleri](active-directory-v2-flows.md).

* [Mobil ve yerel uygulama OAuth 2.0 ile derleme](active-directory-v2-protocols-oauth-code.md)
* [Web oluşturma Open ID uygulamalarla Bağlan](active-directory-v2-protocols-oidc.md)
* [Merhaba ile OAuth 2.0 örtük akışını tek sayfa uygulamaları derleme](active-directory-v2-protocols-implicit.md)
* [Arka plan programları veya sunucu tarafı işlemleri hello ile OAuth 2.0 istemci kimlik bilgileri akışının yapı](active-directory-v2-protocols-oauth-client-creds.md)
* [Merhaba OAuth 2.0 adına akış ile Web API belirteçleri almak](active-directory-v2-protocols-oauth-on-behalf-of.md)
