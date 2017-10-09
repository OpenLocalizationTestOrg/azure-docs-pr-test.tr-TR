---
title: "hello Azure Active Directory v2.0 uç noktası için aaaApp türleri | Microsoft Docs"
description: "uygulamaları ve senaryoları hello Azure Active Directory v2.0 uç noktası tarafından desteklenen Hello türleri."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Hello Azure Active Directory v2.0 uç noktası için uygulama türleri
Hello Azure Active Directory (Azure AD) v2.0 uç noktası kimlik doğrulaması modern uygulama mimarilerinin tümünün endüstri standardı protokollerine dayalı çeşitli destekleyen [OAuth 2.0 veya Openıd Connect](active-directory-v2-protocols.md). Bu makalede hello tercih edilen dilden veya platformdan bağımsız olarak Azure AD v2.0 kullanarak oluşturabileceğiniz uygulama türleri açıklanmaktadır. Merhaba bu makaledeki bilgiler olduğundan, önce üst düzey senaryoları anlamanıza tasarlanmış toohelp [hello kodu ile çalışma başlangıç](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez. mı hello v2.0 uç kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>Merhaba temelleri
Hello hello v2.0 uç noktası kullanan her bir uygulama kaydettirmelisiniz [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com). Merhaba uygulama kayıt işlemi toplar ve uygulamanız için bu değerleri atar:

* Bir **uygulama kimliği** uygulamanızı benzersiz olarak tanımlayan
* A **yeniden yönlendirme URI'si** toodirect yanıtları geri tooyour uygulaması kullanabilirsiniz
* Birkaç diğer senaryoya özel değerler

Ayrıntılar için nasıl çok öğrenin[uygulama kaydetmeyi](active-directory-v2-app-registration.md).

Merhaba uygulama kaydedildikten sonra hello uygulama isteklerini toohello Azure AD v2.0 uç göndererek Azure AD ile iletişim kurar. Açık kaynak çerçeveler ve bu istekleri hello ayrıntılarını işlemek kitaplıklar sunuyoruz. Ayrıca hello seçeneği tooimplement hello kimlik doğrulaması mantığı kendiniz toothese uç noktaları istekleri oluşturarak vardır:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>Web uygulamaları
Bir tarayıcı aracılığıyla kullanıcı erişimleri hello web uygulamaları için (.NET, PHP, Java, Ruby, Python, düğüm), kullandığınız [Openıd Connect](active-directory-v2-protocols.md) kullanıcı oturum açma için. Openıd Connect içinde hello web uygulaması kimliği belirteci alır. Bir kimliği belirteci hello kullanıcının kimliğini doğrular ve talep hello biçiminde hello kullanıcı hakkında bilgi sağlayan bir güvenlik belirteci şöyledir:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Merhaba kullanılabilir tooan uygulamada olan talepler ve belirteç tüm hello türleri hakkında bilgi edinebilirsiniz [v2.0 belirteçler başvuru](active-directory-v2-tokens.md).

Web sunucusu uygulamalarında hello oturum açma kimlik doğrulaması akışı üst düzey adımları gerçekleştirir:

![Web uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

Merhaba v2.0 uç noktasından alınan bir ortak imzalama anahtarı ile Merhaba kimliği belirteci doğrulayarak hello kullanıcının kimliğini emin olabilirsiniz. Sonraki sayfa isteklerinde kullanılan tooidentify hello kullanıcı olabilen bir oturum tanımlama bilgisi ayarlanır.

toosee eylemi, oturum açma hello web uygulama kodunuzda birini deneyin içinde bu senaryo örnekleri bizim v2.0 [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.

Ayrıca toosimple oturum açma, bir web sunucusu uygulamasının bir REST API'si gibi başka bir web hizmeti tooaccess gerekebilir. Bu durumda, hello kullanarak hello web sunucusu uygulamasının birleşik bir Openıd Connect ve OAuth 2.0 akışı, prosese [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols.md). Bu senaryo hakkında daha fazla bilgi için bilgiyi [web uygulamaları ve Web API ile çalışmaya başlama](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>Web API'leri
Merhaba v2.0 uç noktası toosecure web Hizmetleri, uygulamanızın RESTful Web API'si gibi kullanabilirsiniz. Kimlik belirteçlerini ve oturum tanımlama bilgileri yerine, bir Web API bir OAuth 2.0 erişim belirteci toosecure, veri ve tooauthenticate kullanır gelen istekleri. Web API Hello çağıran bir erişim belirteci bu gibi bir HTTP isteğinin hello yetkilendirme üstbilgisinde ekler:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Merhaba Web API hello çağrıyı yapandan hello erişim belirteçte kodlanmış taleplere hakkında hello erişim belirteci tooverify hello API çağıranının kimliğini ve tooextract bilgileri kullanır. toolearn kullanılabilir tooan uygulamasına talepler ve belirteç tüm hello türleri hakkında bkz hello [v2.0 belirteçler başvuru](active-directory-v2-tokens.md).

Bir Web API kullanıcılar hello güç tooopt verin veya belirli işlevleri veya veri yetersiz izinler olarak da bilinen göstererek opt [kapsamları](active-directory-v2-scopes.md). Bir arama uygulaması tooacquire izin tooa kapsam için bir akışı sırasında toohello kapsam hello kullanıcı onaylaması gerekir. Merhaba v2.0 uç hello kullanıcı izni ister ve Web API alır, hello'da tüm erişim belirteçleri izinleri kaydeder. Merhaba Web API her çağrıda alır ve yetkilendirme denetimleri gerçekleştirir hello erişim belirteci doğrular.

Bir Web API uygulamaları, web sunucu uygulamaları, masaüstü ve mobil uygulamalar, tek sayfa uygulamaları, sunucu tarafı deamon'lar ve hatta diğer Web API'leri dahil olmak üzere tüm türlerinden erişim belirteçleri alabilir. Merhaba üst düzey Akış Web API'si şöyle görünür:

![Web API kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toosecure OAuth2 erişim belirteçleri, hello Web API kodunda kullanıma kullanarak bir Web API'sini nasıl örnekleri toolearn bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.

Çoğu durumda, web API'leri da aşağı tooother web API'leri Azure Active Directory tarafından güvenli hale getirilmiş toomake Giden istekleri gerekir.  toodo bu nedenle, web API'leri, Azure AD yararlanabilir **adına, üzerinde** hello web API tooexchange giden isteklerinde kullanılan başka bir erişim belirteci toobe için gelen bir erişim belirteci verir akış.  Merhaba v2.0 uç noktanın akış adına açıklanan [burada ayrıntı](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>Mobil ve yerel uygulamalar
Mobil ve Masaüstü uygulamaları gibi cihaz yüklü uygulamalar genellikle tooaccess arka uç hizmetlerine veya Web API'leri, verilerini depolamak ve bir kullanıcı adına işlevleri gerçekleştirmek gerekir. Bu uygulamaları hello kullanarak oturum açma ve yetkilendirme tooback uç hizmetlerinin ekleyebilirsiniz [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols-oauth-code.md).

Merhaba kullanıcı oturum açtığında bu akışta hello uygulama hello v2.0 uç noktasından bir yetkilendirme kodu alır. Yetkilendirme kodu temsil hello uygulamanın izni toocall arka uç hizmetlerinin oturum hello kullanıcı adına hello. Merhaba uygulama hello yetkilendirme kodu hello arka planda bir OAuth 2.0 erişim belirteci ve bir yenileme belirteci değiştirebilir. Merhaba uygulama HTTP isteklerinde hello erişim belirteci tooauthenticate tooWeb API'leri kullanın ve eski erişim belirteçleri sona erdiğinde hello yenileme belirteci tooget yeni erişim belirteçleri kullanın.

![Yerel uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>Tek sayfa uygulamaları (JavaScript)
Birçok modern uygulamanın, JavaScript'te öncelikli olarak yazılmış tek sayfa uygulaması ön ucu sahip. Sıklıkla AngularJS, Ember.js veya Durandal.js gibi framework kullanılarak yazılır. Hello Azure AD v2.0 uç hello kullanarak bu uygulamaları destekler [OAuth 2.0 örtük akışını](active-directory-v2-protocols-implicit.md).

Bu akışta hello uygulama belirteçlerini doğrudan hello alır v2.0 uç noktası, herhangi bir sunucudan sunucuya alışverişleri olmadan yetkilendirmek. Tüm kimlik doğrulaması mantığı ve gerçekleştirilen işlemlerin işleme oturumu tamamen ek sayfa yeniden yönlendirmeleri olmadan hello JavaScript istemci yerleştirin.

![Örtük kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee eylem, bu senaryoda hello tek sayfalı uygulama kodu örneklerinden birini deneyin bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.

## <a name="daemons-and-server-side-apps"></a>Arka plan programları ve sunucu tarafı uygulamalar
Uzun süre çalışan işlemler olması veya, bir kullanıcı etkileşimi olmadan çalışan uygulamalar da Web API'leri gibi kaynaklar tooaccess güvenli bir yol gerekir. Bu uygulamaları kimlik doğrulaması ve hello uygulamanın kimliğini kullanarak belirteçleri almak yerine bir kullanıcı kimliğiyle hello OAuth 2.0 istemci kimlik bilgileri akışının temsilcisi.

Bu akışta hello uygulama hello ile doğrudan etkileşim `/token` uç nokta tooobtain uç noktalar:

![Arka plan programı uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild bir arka plan programı uygulaması bkz hello istemci kimlik bilgileri belgelerinde bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümünde veya deneyin bir [.NET örnek uygulaması](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
