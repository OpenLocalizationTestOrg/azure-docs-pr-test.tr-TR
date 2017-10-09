---
title: aaaAzure AD B2C | Microsoft Docs
description: "Uygulama Hello türlerini hello Azure Active Directory B2C oluşturabilirsiniz."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C: Uygulama türleri
Azure Active Directory (Azure AD) B2C, çeşitli modern uygulama mimarilerine yönelik kimlik doğrulamasını destekler. Bunların tümünün hello endüstri standardı protokollerine dayalıdır [OAuth 2.0](active-directory-b2c-reference-protocols.md) veya [Openıd Connect](active-directory-b2c-reference-protocols.md). Bu belgede kısaca hello oluşturabileceğiniz uygulama türleri açıklanmaktadır, hello dilden veya platformdan bağımsız tercih ettiğiniz. Ayrıca, önce hello üst düzey senaryoları anlamanıza yardımcı olur [uygulamaları oluşturmaya başlayın](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>Merhaba temelleri
Azure AD B2C kullanan her uygulamanın kaydedilmelidir, [B2C dizini](active-directory-b2c-get-started.md) hello aracılığıyla [Azure Portal](https://portal.azure.com/). Merhaba uygulama kayıt işlemi toplar ve birkaç değerleri tooyour uygulama atar:

* Uygulamanızı benzersiz olarak tanımlayan bir **Uygulama Kimliği**.
* A **yeniden yönlendirme URI'si** kullanılan toodirect yanıtları geri tooyour uygulama olabilir.
* Tüm diğer senaryoya özel değerler. Daha fazla ayrıntı için nasıl çok öğrenin[uygulama kaydetmeyi](active-directory-b2c-app-registration.md).

Merhaba uygulama kaydedildikten sonra Azure AD ile istekleri toohello Azure AD v2.0 uç göndererek iletişim kurar:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

TooAzure AD B2C gönderilen her isteği belirtir bir **İlkesi**. Bir ilke hello Azure AD davranışını denetler. Bu uç noktaları toocreate kullanıcı deneyimlerini büyük ölçüde özelleştirilebilir bir dizi de kullanabilirsiniz. Ortak ilkelere kaydolma, oturum açma ve profil düzenleme ilkeleri dahildir. İlkeleriyle bilmiyorsanız, Azure AD B2C hello hakkında okumalısınız [Genişletilebilir ilke çerçevesini](active-directory-b2c-reference-policies.md) devam etmeden önce.

Merhaba etkileşim her uygulamanın v2.0 uç noktası benzer bir üst düzey deseni izler:

1. Merhaba uygulama hello kullanıcı toohello v2.0 uç noktası tooexecute yönlendiren bir [İlkesi](active-directory-b2c-reference-policies.md).
2. Merhaba kullanıcı hello İlkesi toohello ilke tanımına göre tamamlar.
3. Merhaba uygulama hello v2.0 uç noktasından bir tür güvenlik belirteci alır.
4. Merhaba uygulama hello güvenlik belirteci tooaccess korumalı bilgileri veya korunan bir kaynağa kullanır.
5. Merhaba kaynak sunucusuna erişim izni hello güvenlik belirteci tooverify doğrular.
6. Merhaba uygulama hello güvenlik belirtecini düzenli aralıklarla yeniler.

<!-- TODO: Need a page for libraries toolink too-->
Bu adımları biraz Merhaba, oluşturduğunuz uygulama türüne göre farklı olabilir. Açık kaynak kitaplıkları, sizin için hello ayrıntıları ele alabilir.

## <a name="web-apps"></a>Web uygulamaları
Azure AD B2C, bir sunucuda barındırılan ve tarayıcı aracılığıyla erişilen web uygulamalarında (.NET, PHP, Java, Ruby, Python ve Node.js dahil) tüm kullanıcı deneyimleri için [OpenID Connect](active-directory-b2c-reference-protocols.md)'i destekler. Buna oturum açma, kaydolma ve profil yönetimi dahildir. Openıd Connect Hello Azure AD B2C uygulamasında web uygulamanız kimlik doğrulama isteklerini tooAzure AD vererek bu kullanıcı deneyimlerini başlatır. Merhaba isteği Hello sonucu bir `id_token`. Bu güvenlik belirteci hello kullanıcının kimliğini temsil eder. Ayrıca, talep hello biçiminde hello kullanıcı hakkında bilgi sağlar:

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Merhaba belirteçleri ve talepleri kullanılabilir tooan uygulamada hello türleri hakkında daha fazla bilgi [B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md).

Bir web uygulamasında, her bir [ilke](active-directory-b2c-reference-policies.md) yürütme işlemi şu üst düzey adımları uygular:

![Web Uygulaması Kulvarları Görüntüsü](./media/active-directory-b2c-apps/webapp.png)

Merhaba doğrulanması `id_token` Azure AD'den alınan bir ortak imzalama anahtarı kullanarak yeterli tooverify hello hello kullanıcı kimliğidir. Bu ayrıca sonraki sayfa isteklerinde kullanılan tooidentify hello kullanıcıya bir oturum tanımlama bilgisi ayarlar.

toosee eylem, bu senaryoda hello web uygulaması oturum açma kodu örneklerinden birini deneyin bizim [Başlarken bölümü](active-directory-b2c-overview.md#get-started).

Toplama toofacilitating basit oturum açma içinde bir web sunucusu uygulaması tooaccess bir arka uç web hizmeti de gerekebilir. Bu durumda, başlangıç web uygulaması biraz farklı gerçekleştirebilirsiniz [Openıd Connect akışı](active-directory-b2c-reference-oidc.md) yetkilendirme kodları kullanarak belirteçleri almak ve yenileme belirteçleri. Bu senaryo hello aşağıda gösterilen [Web API'leri bölümünde](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>Web API'leri
Azure AD B2C toosecure web Hizmetleri, uygulamanızın RESTful web API'si gibi kullanabilirsiniz. Web API'leri, kendi veri belirteçleri kullanarak gelen HTTP isteklerini kimlik doğrulaması yaparak OAuth 2.0 toosecure kullanabilirsiniz. web API'si çağıranı Hello hello authorization üstbilgisi bir HTTP isteğinin bir belirteç ekler:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Merhaba web API sonra hello çağrıyı yapandan hello belirteçte kodlanmış taleplere hakkında hello belirteci tooverify hello API Arayanın kimlik ve tooextract bilgileri kullanabilirsiniz. Merhaba belirteçleri ve talepleri kullanılabilir tooan uygulamada hello türleri hakkında daha fazla bilgi [Azure AD B2C belirteç başvurusunda](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Azure AD B2C şu anda yalnızca kendi iyi bilinen istemcileri aracılığıyla erişilen web API'lerini desteklemektedir. Örneğin, tam uygulamanız bir iOS uygulaması, Android uygulaması ve arka uç web API'si içerebilir. Bu mimari tam olarak desteklenir. Başka bir iOS uygulaması gibi bir iş ortağı istemcisine izin vererek tooaccess aynı web API şu anda desteklenmeyen hello. Tam uygulamanızın hello bileşenlerinin tümünü tek bir uygulama kimliği paylaşması gerekir
>
>

Web API'si; web uygulamaları, masaüstü ve mobil uygulamalar, tek sayfa uygulamaları, sunucu tarafı daemon'ları ve diğer web API'leri dahil olmak üzere birçok istemci türünden belirteç alabilir. Merhaba tam Akış web API'si çağıran bir web uygulaması için bir örneği burada verilmiştir:

![Web Uygulaması Web API'si Kulvarları Görüntüsü](./media/active-directory-b2c-apps/webapi.png)

Yetkilendirme kodları, yenileme belirteçleri ve belirteç alma hello adımları hakkında daha fazla toolearn okuma hakkında hello [OAuth 2.0 protokolünü](active-directory-b2c-reference-oauth-code.md).

Azure AD B2C, hello kullanıma kullanarak bir web API toosecure web API'si eğitimlerine nasıl toolearn bizim [Başlarken bölümü](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>Mobil ve yerel uygulamalar
Mobil ve Masaüstü uygulamaları gibi cihazlara yüklenen uygulamaların çoğunlukla tooaccess arka uç hizmetlerine veya web API'lerine kullanıcılar adına gerekir. Özelleştirilmiş kimlik yönetimi deneyimleri tooyour yerel uygulamalar ekleyin ve güvenli bir şekilde Azure AD B2C ve hello kullanarak arka uç hizmetlerini çağırma [OAuth 2.0 yetkilendirme kodu akışını](active-directory-b2c-reference-oauth-code.md).  

Bu akışta hello uygulama yürütür [ilkeleri](active-directory-b2c-reference-policies.md) ve alan bir `authorization_code` hello kullanıcı hello İlkesi tamamlandıktan sonra Azure AD'den. Merhaba `authorization_code` hello uygulamanın izni toocall arka uç hizmetlerinin şu anda açık olan hello kullanıcı adına temsil eder. Merhaba uygulama sonra hello exchange `authorization_code` hello arka planda bir `id_token` ve `refresh_token`.  Merhaba uygulama hello kullanabilir `id_token` tooauthenticate tooa arka uç web API HTTP istekleri. Merhaba kullanabilirsiniz `refresh_token` tooget yeni bir `id_token` daha eski bir süresi dolduğunda.

> [!NOTE]
> Azure AD B2C, bir uygulamanın kendi arka uç web hizmeti şu anda kullanılan tooaccess olan belirteçleri destekler. Örneğin, tam uygulamanız bir iOS uygulaması, Android uygulaması ve arka uç web API'si içerebilir. Bu mimari tam olarak desteklenir. İOS uygulama tooaccess OAuth 2.0 erişim belirteçleri kullanarak bir iş ortağı web API'sine izin verme şu anda desteklenmiyor. Tam uygulamanızın hello bileşenlerinin tümünü tek bir uygulama kimliği paylaşması gerekir
>
>

![Yerel Uygulama Kulvarları Görüntüsü](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Geçerli sınırlamalar
Azure AD B2C hello şu uygulama türlerini şu anda desteklemiyor, ancak hello yol haritası üzerinde etmektedir. 

### <a name="daemonsserver-side-apps"></a>Daemon'lar/sunucu tarafı uygulamalar
Uzun süre çalışan işlemler içeren veya kullanıcı hello varlığını çalışan uygulamalar da web API'leri gibi kaynakları tooaccess güvenli bir yol gerekir. Bu uygulamalar, kimlik doğrulaması ve hello uygulamanın kimliğini (bir kullanıcının Devredilmiş kimliği yerine) kullanarak ve hello OAuth 2.0 istemci kimlik bilgileri akışını kullanarak belirteçleri alın.

Bu akış şu anda Azure AD B2C tarafından desteklenmemektedir. Bu uygulamalar ancak etkileşimli kullanıcı akışı gerçekleştikten sonra belirteç alabilir.

### <a name="web-api-chains-on-behalf-of-flow"></a>Web API'si zincirleri (temsili akış)
Birçok mimarisi, burada her ikisi de Azure AD B2C tarafından güvenliği sağlanan başka bir aşağı akış web API'si, web toocall gereken API içerir. Bu senaryo, Web API'si arka ucuna sahip yerel istemcilerde yaygındır. Bu, daha sonra hello Azure AD grafik API'si gibi bir Microsoft online service çağırır.

Bu Zincirli web API'si senaryosu olarak da bilinen hello üzerinde-temsili akış hello OAuth 2.0 JWT taşıyıcı kimlik bilgisi yetkisi kullanılarak desteklenebilir.  Ancak, hello üzerinde-temsili akış şu anda hello Azure AD B2C uygulanmadı.
