---
title: "Azure AD v2.0 tarafından desteklenen yetkilendirme protokolleri hakkında bilgi edinin | Microsoft Docs"
description: "Azure AD v2.0 uç noktası tarafından desteklenen protokolleri Kılavuzu."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mtillman
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
ms.openlocfilehash: ce9a7cb14b933da23873d69e1f14a744d012a858
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="v20-protocols---oauth-20--openid-connect"></a>v2.0 protokolleri - OAuth 2.0 & Openıd Connect
V2.0 uç noktası kimlik olarak-hizmet endüstri standardı protokolleri, Openıd Connect ve OAuth 2.0 ile Azure AD kullanabilirsiniz.  Hizmet standartlara uygun olsa da, bu protokollerin herhangi iki uygulamaları arasındaki küçük farklılıklar olabilir.  Burada yer alan bilgiler doğrudan göndererek kodunuzu yazmak seçtiğiniz & işleme HTTP isteklerini veya kullanımı bir 3. taraf açma bizim açık kaynak kitaplıkları birini kullanmak yerine Kaynak Kitaplığı yararlı olacaktır.
<!-- TODO: Need link to libraries above -->

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.  V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>
>

## <a name="the-basics"></a>Temel kavramları
Neredeyse tüm OAuth ve Openıd Connect akışlarında, Exchange'de ilgili dört tarafların vardır:

![OAuth 2.0 rolleri](../../media/active-directory-v2-flows/protocols_roles.png)

* **Yetkilendirme sunucusu** v2.0 uç noktası.  Kullanıcının kimliğini sağlayarak, verme ve kaynaklara erişimi iptal etme ve belirteç için sorumlu değildir.  Kimlik sağlayıcısı olarak da bilinen olduğu -, güvenli bir şekilde kullanıcının bilgileri, erişimleri ve bir akışı taraflar arasında güven ilişkileri ile yapmak için herhangi bir şey işleme.
* **Kaynak sahibi** genellikle son kullanıcı'dır.  Verilerin sahibi ve bu veri ya da kaynağa erişmek için üçüncü taraf izin vermek için güç olan taraf olur.
* **OAuth istemcisi** kendi uygulama kimliği ile tanımlanan uygulamanızın  Genellikle son kullanıcı ile etkileşime giren taraf olur ve yetkilendirme sunucusundan belirteçleri ister.  İstemci kaynak sahibi tarafından kaynağa erişim izni verilmesi gerekir.
* **Kaynak sunucusu** kaynak veya veri bulunduğu değil.  Güvenli bir şekilde kimlik doğrulaması ve OAuth istemcisi yetkilendirmek için yetkilendirme sunucusu güvenir ve taşıyıcı access_tokens bir kaynağa erişim izni olduğundan emin olmak için kullanır.

## <a name="app-registration"></a>Uygulama kaydı
V2.0 uç noktası kullanan her uygulamanın kayıtlı gerekir [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) OAuth veya Openıd Connect kullanarak etkileşim kurabilen önce.  Uygulama kayıt işlemi Topla & uygulamanıza birkaç değerler atayın:

* Bir **uygulama kimliği** uygulamanızı benzersiz olarak tanımlayan
* A **yeniden yönlendirme URI'si** veya **paket tanımlayıcı** yanıtları uygulamanıza geri yönlendirmek için kullanılabilir
* Diğer birkaç senaryoya özel değerler.

Daha ayrıntılı bilgi için [uygulama kaydetmeyi](active-directory-v2-app-registration.md) öğrenin.

## <a name="endpoints"></a>Uç Noktalar
Kaydedildikten sonra uygulamanın v2.0 uç noktasına istek göndererek Azure AD ile iletişim kurar:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Burada `{tenant}` dört farklı değerler birini alabilir:

| Değer | Açıklama |
| --- | --- |
| `common` |Azure Active Directory'den uygulamasına imzalamak için hem kişisel Microsoft hesapları hem de iş/Okul hesapları olan kullanıcıların sağlar. |
| `organizations` |Yalnızca iş/Okul hesapları olan kullanıcılar için uygulamaya imzalamak için Azure Active Directory izin verir. |
| `consumers` |Yalnızca kullanıcıların kişisel Microsoft hesaplarıyla uygulamasına imzalamak için (MSA) sağlar. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` veya `contoso.onmicrosoft.com` |Yalnızca iş/Okul hesapları olan kullanıcılar için uygulamaya imzalamak için belirli bir Azure Active Directory Kiracı izin verir.  Azure AD kiracısı kolay etki alanı adı ya da kiracının GUID tanımlayıcısı kullanılabilir. |

Bu uç noktalar ile etkileşim hakkında daha fazla bilgi için aşağıdaki belirli uygulama türünü seçin.

## <a name="tokens"></a>Belirteçler
OAuth 2.0 ve Openıd Connect v2.0 uyarlamasını taşıyıcı belirteçler, taşıyıcı belirteçlerini Jwt'ler temsil dahil olmak üzere kapsamlı kullanımını olun. Bir taşıyıcı belirteci korunan bir kaynağa "bearer" erişim veren bir basit güvenlik belirtecidir. Bu anlamda belirteç sunabilir herhangi bir tarafa "bearer" dir. İletim ve depolama belirteçte güvenli hale getirmek için gerekli adımları katılmaz varsa bir taraf ilk taşıyıcı belirteci almak için Azure AD ile kimlik doğrulaması yapması gereken ancak ele ve istenmeyen bir şahıs tarafından kullanılır. Bazı güvenlik belirteçleri kullanarak gelen yetkisiz tarafların engellemek için yerleşik bir mekanizma olmakla birlikte, taşıyıcı belirteçlerini bu düzenek yoksa ve Aktarım Katmanı Güvenliği (HTTPS) gibi güvenli bir kanal taşınan gerekir. Bir taşıyıcı belirteci açık bir şekilde iletilirse, bir adam-Orta saldırı kötü amaçlı bir tarafın belirtecini almak ve bir yetkisiz erişim korunan bir kaynağa için kullanmak üzere kullanılabilir. Depolama veya taşıyıcı belirteçlerini daha sonra kullanmak için önbelleğe alma aynı güvenlik ilkeleri uygulayın. Her zaman uygulamanızı aktarır ve güvenli bir şekilde taşıyıcı belirteçleri depolar emin olun. Taşıyıcı belirteçlerini hakkında daha fazla güvenlik konuları için bkz: [RFC 6750 bölüm 5](http://tools.ietf.org/html/rfc6750).

Belirteçleri v2.0 uç kullanılır farklı türdeki daha ayrıntılı bilgi sağlanmıştır [v2.0 uç noktası belirteç başvurusu](active-directory-v2-tokens.md).

## <a name="protocols"></a>Protokoller
Bazı örnek isteklerini görmek için hazır olduğunuzda, biri ile çalışmaya başlama öğreticileri aşağıda.  Her biri bir belirli kimlik doğrulama senaryosu karşılık gelir.  Sizin için doğru akış olduğu saptarken yardıma gerek duyarsanız kullanıma [v2.0 oluşturabilir uygulama türlerini](active-directory-v2-flows.md).

* [Mobil ve yerel uygulama OAuth 2.0 ile derleme](active-directory-v2-protocols-oauth-code.md)
* [Web oluşturma Open ID uygulamalarla Bağlan](active-directory-v2-protocols-oidc.md)
* [OAuth 2.0 örtük akışını ile tek sayfa uygulamaları derleme](active-directory-v2-protocols-implicit.md)
* [Yapı Daemon veya OAuth 2.0 istemci kimlik bilgileri ile sunucu tarafı işlemlerini akış](active-directory-v2-protocols-oauth-client-creds.md)
* [OAuth 2.0 adına akış ile Web API belirteçleri almak](active-directory-v2-protocols-oauth-on-behalf-of.md)
