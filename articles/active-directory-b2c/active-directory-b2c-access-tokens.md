---
title: "Azure Active Directory B2C: İsteyen erişim belirteçleri | Microsoft Docs"
description: "Bu makale size nasıl gösterir toosetup bir istemci uygulaması ve bir erişim belirteci edinmek."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: İsteyen erişim belirteçleri

Bir erişim belirteci (olarak gösterilen **erişim\_belirteci** Azure AD B2C hello yanıtlarındaki) tarafından güvenliği sağlanan bir istemci tooaccess kaynakları kullanabilir güvenlik belirteci biçimidir bir [yetkilendirme sunucusu](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), web API'si gibi. Erişim belirteci olarak temsil [Jwt'ler](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) ve hello hedeflenen kaynak sunucu ve hello izin verilenler toohello sunucu hakkındaki bilgileri içerir. Hello kaynak sunucusu çağrılırken hello erişim belirteci hello HTTP isteğinde bulunması gerekir.

Bu makalede nasıl tooobtain tooconfigure bir istemci uygulaması ve web API'si için sipariş ele bir **erişim\_belirteci**.

> [!NOTE]
> **Web API'si zincirleri (üzerinde-adına-ın) Azure AD B2C tarafından desteklenmiyor.**
>
> Birçok mimarisi web toocall gereken API başka bir aşağı akış web API'si içerir, hem Azure AD B2C tarafından güvence altına. Bu senaryo, sırayla hello Azure AD grafik API'si gibi bir Microsoft online service çağıran bir web API'si arka ucuna sahip yerel istemcilerde yaygındır.
>
> Bu Zincirli web API'si senaryosu hello üzerinde-temsili akış bilinen OAuth 2.0 JWT taşıyıcı kimlik bilgisi grant, aksi takdirde hello kullanarak desteklenebilir. Ancak, hello üzerinde-temsili akış şu anda Azure AD B2C'de uygulanmamıştır.

## <a name="register-a-web-api-and-publish-permissions"></a>Web API'si kaydetmek ve izinleri yayımlama

Bir erişim belirteci istemeden önce ilk tooregister web API gerekir ve toohello istemci uygulaması verilebilir izinleri (kapsam) yayımlayın.

### <a name="register-a-web-api"></a>Web API’si kaydetme

1. Merhaba B2C özellikleri dikey penceresinde hello Azure portal, tıklatın **uygulamaları**.
1. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
1. Girin bir **adı** uygulama tooconsumers anlatmaktadır Merhaba uygulaması için. Örneğin, "Contoso API" girebilirsiniz.
1. İki durumlu hello **web uygulaması eklemek veya web API'si** çok geçiş**Evet**.
1. Merhaba rasgele bir değer girin **yanıt URL'leri**. Örneğin, `https://localhost:44316/` girin. bir API hello belirteci doğrudan Azure AD B2C almalıdır değil bu yana hello değeri önemli değildir.
1. Bir **Uygulama Kimliği URI'si** girin. Bu web API için kullanılan hello tanımlayıcısıdır. Örneğin, 'Not' hello kutusuna girin. Merhaba **uygulama kimliği URI'si** sonra olacaktır `https://{tenantName}.onmicrosoft.com/notes`.
1. Tıklatın **oluşturma** tooregister uygulamanızı.
1. Yeni oluşturduğunuz hello uygulama'yı tıklatın ve Kopyala hello genel benzersiz **uygulama istemci Kimliğini** daha sonra kodunuzda kullanacağınız.

### <a name="publishing-permissions"></a>Yayımlama izinleri

Uygulamanızı bir API çağrılırken benzer toopermissions olan kapsam gereklidir. Bazı kapsamlar "Okuma" veya "yazma" olarak gösterilebilir. Web veya çok API'den "Okuma" Yerel uygulama istediğinizi varsayalım. Uygulamanızı Azure AD B2C çağırırdı ve bir erişim belirteci isteği erişim toohello kapsamı "Okuma" verir. Azure AD B2C tooemit böyle bir erişim belirteci için sırayla hello uygulamasının toobe izni çok "Merhaba belirli API'SİNDEN okuma" izni gerekiyor. toodo bunu API'nizi ilk olarak toopublish hello "Okuma" kapsam gereksinimi vardır.

1. Hello Azure AD B2C içinde **uygulamaları** dikey penceresinde, açık hello web API uygulamasını ("Contoso API").
1. **Yayımlanan kapsamlar**’a tıklayın. Tooother uygulamaları verilebilir hello izinleri (kapsam) tanımladığınız budur.
1. Ekleme **kapsam değerleri** gerektiğinde (örneğin, "Okuma"). Varsayılan olarak, hello "user_impersonation" kapsam tanımlanır. İsterseniz, bu göz ardı edebilirsiniz. Hello hello kapsam için bir açıklama girin **kapsam adı** sütun.
1. **Kaydet** düğmesine tıklayın.

> [!IMPORTANT]
> Merhaba **kapsam adı** hello hello açıklamasıdır **kapsam değeri**. Merhaba kapsam kullanırken emin toouse hello yapmanız **kapsam değeri**.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>Yerel vermek veya web uygulama izinleri tooa web API'si

Bir API yapılandırılmış toopublish kapsamları eklendiğinde, bu kapsamları hello Azure portal aracılığıyla verilen toobe Merhaba istemci uygulaması gerekir.

1. Toohello gidin **uygulamaları** hello B2C özellikleri Dikey Menüde.
1. Bir istemci uygulaması kaydetmek ([web uygulaması](active-directory-b2c-app-registration.md#register-a-web-app) veya [yerel istemci](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) zaten yoksa. Bu kılavuz, başlangıç noktası olarak izliyorsanız, tooregister bir istemci uygulaması gerekir.
1. Tıklayın **API erişimini**.
1. **Ekle**'ye tıklayın.
1. Web API ve hello kapsamı (toogrant istediğiniz izinleri) seçin.
1. **Tamam** düğmesine tıklayın.

> [!NOTE]
> Azure AD B2C, istemci uygulama kullanıcıları kendi onaylarının istemez. Bunun yerine, tüm onay, yukarıda açıklanan hello uygulamalar arasında yapılandırılmış hello izinlere dayalı hello Yöneticisi tarafından sağlanır. Bir uygulama için bir izin verme iptal edilirse, daha önce mümkün tooacquire olan tüm kullanıcılar bu izni artık mümkün toodo kadar olabilir.

## <a name="requesting-a-token"></a>Bir belirteç isteme

Bir erişim belirteci isterken hello istemci uygulamanın hello toospecify istenen hello izinleri ihtiyaç **kapsam** hello isteğinin parametresi. Örneğin, toospecify hello **kapsam değeri** "Merhaba hello sahip API okuma" **uygulama kimliği URI'si** , `https://contoso.onmicrosoft.com/notes`, hello kapsam olacaktır `https://contoso.onmicrosoft.com/notes/read`. Bir yetkilendirme kodu isteği toohello örneği aşağıdadır `/authorize` uç noktası.

> [!NOTE]
> Şu anda, özel etki alanlarını erişim belirteçleri ile birlikte desteklenmez. Merhaba istek URL'si tenantName.onmicrosoft.com etki alanınızda kullanmanız gerekir.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire hello birden çok izinler aynı isteği, birden çok giriş hello tek ekleyebilirsiniz **kapsam** boşluklarla ayırarak parametresi. Örneğin:

Kodunu çözdü URL'si:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

Kodlanmış URL'si:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

İstemci uygulamanız için verilen değerinden bir kaynak için daha fazla kapsam (izinleri) isteyebilir. Bu hello durum böyle olduğunda, en az bir izin verilirse hello çağrı başarılı olur. Merhaba kaynaklanan **erişim\_belirteci** başarıyla verilmiş yalnızca hello izinlerle doldurulmuş kendi "scp" talep sahip olur.

> [!NOTE] 
> İki farklı web kaynaklarına karşı isteyen izinleri hello desteklemiyoruz aynı isteği. Bu tür bir istek başarısız olur.

### <a name="special-cases"></a>Özel durumlar

Merhaba Openıd Connect standart özel "scope" değerlerden belirtir. Özel kapsamları temsil hello izni çok aşağıdaki "Merhaba kullanıcının profilini erişim" Merhaba:

* **openıd**: Bu bir kimliği belirteci istekleri
* **Çevrimdışı\_erişim**: Bu bir yenileme belirteci istekleri (kullanarak [kimlik doğrulama kodu akar](active-directory-b2c-reference-oauth-code.md)).

Merhaba, `response_type` parametresinde bir `/authorize` istek içerir `token`, hello `scope` parametresi en az bir kaynak kapsam içermelidir (dışında `openid` ve `offline_access`), verilecektir. Aksi takdirde hello `/authorize` istek bir hata ile sonlandırılacak.

## <a name="hello-returned-token"></a>Merhaba belirteç döndürdü

Başarıyla minted içinde **erişim\_belirteci** (ya da hello gelen `/authorize` veya `/token` uç nokta), hello aşağıdaki talep olacaktır mevcut:

| Ad | İste | Açıklama |
| --- | --- | --- |
|Hedef kitle |`aud` |Merhaba **uygulama kimliği** hello tek kaynak hello belirtecini erişim verir. |
|Kapsam |`scp` |Merhaba, toohello kaynak izinler. Birden çok izin verilenler boşlukla ayrılmış. |
|Yetkili taraf |`azp` |Merhaba **uygulama kimliği** hello istek başlatılan hello istemci uygulamasının. |

Ne zaman API'nizi alır hello **erişim\_belirteci**, aşağıdakileri yapmalıdır [hello belirtecini doğrula](active-directory-b2c-reference-tokens.md) belirteci hello tooprove gerçek ve hello doğru talep sahiptir.

Her zaman açık toofeedback ve öneriler duyuyoruz! Bu konu ile yaşarsanız hello etiketini kullanarak yığın taşması sonrası ['azure ad b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c). Özellik istekleri için çok eklemediğiniz[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

## <a name="next-steps"></a>Sonraki adımlar

* Bir web API kullanarak yapı [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)
* Bir web API kullanarak yapı [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)
