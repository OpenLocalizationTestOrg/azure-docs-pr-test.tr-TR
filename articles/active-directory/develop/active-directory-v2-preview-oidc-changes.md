---
title: "aaaChanges toohello Azure AD v2.0 uç | Microsoft Docs"
description: "Toohello uygulama modeli v2.0 Genel Önizleme protokolleri yapılan değişikliklerin bir açıklaması."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>Önemli güncelleştirmeleri toohello v2.0 kimlik doğrulama protokolleri
Uyarı geliştiriciler! Merhaba sonraki iki hafta biz birkaç güncelleştirmeleri bizim Önizleme dönemi boyunca yazılmış uygulamalar için önemli değişiklikler olduğu anlamına gelebilir tooour v2.0 kimlik doğrulama protokolleri yapacak.  

## <a name="who-does-this-affect"></a>Kimin bu etkiliyor mu?
Toouse hello v2.0 yazılmış uygulamalar kimlik doğrulama uç noktası Yakınsanan,

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Merhaba v2.0 uç noktası hakkında daha fazla bilgi bulunabilir [burada](active-directory-appmodel-v2-overview.md).

Bizim Openıd Connect veya OAuth web middlewares birini kullanarak doğrudan toohello v2.0 protokol kodlayarak hello v2.0 uç kullanarak bir uygulama oluşturduktan ya da 3 diğer taraf kitaplıklar tooperform kimlik doğrulamasını kullanarak, olmalısınız yapma ve projeleri tootest hazır gerekirse değiştirir.

## <a name="who-doesnt-this-affect"></a>Kimin bu etkilemez?
Merhaba üretim Azure AD kimlik doğrulama uç noktası karşı yazılan tüm uygulamalar

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Bu protokol taş ayarlanır ve herhangi bir değişiklik yaşayan değil.

Ayrıca, uygulamanızı **yalnızca** bizim ADAL kitaplığı tooperform kimlik doğrulaması kullanan toochange hiçbir şey olmaz.  ADAL hello değişiklikleri uygulamanızdan tam korumalı.  

## <a name="what-are-hello-changes"></a>Merhaba değişiklikleri nelerdir?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Merhaba x5t değeri JWT üstbilgileri kaldırma
Merhaba v2.0 uç hello belirteci hakkında ilgili meta veriler üstbilgi parametreleri bölümüyle içerir JWT belirteçleri yaygın, kullanır.  Bizim geçerli Jwt'ler birini hello üstbilgisinin kod çözme, aşağıdakine benzer bulur:

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Her iki hello "x5t" ve "çocuk" özelliklerini hello ortak anahtarı burada tanımlayın, kullanılan toovalidate hello belirtecinin imzası hello Openıd Connect meta veri uç noktasından alınan olması gerekir.

Burada yapıyoruz hello değişiklik tooremove hello "x5t" özelliğidir.  Aynı mekanizmaları toovalidate belirteçler, ancak yalnızca hello "çocuk" özelliği tooretrieve hello doğru ortak anahtar üzerinde belirtilen hello Openıd Connect Protokolü yararlanmalıdır toouse hello devam edebilir. 

> [!IMPORTANT]
> **İşinizi: uygulamanızı hello x5t değeri hello varlığını bağlı değildir emin olun.**
> 
> 

### <a name="removing-profileinfo"></a>Profile_info kaldırma
Daha önce hello v2.0 uç base64 ile kodlanmış JSON nesnesi adı verilen belirteç yanıtları döndürme `profile_info`.  Bir erişim belirteci hello v2.0 uç noktasından bir istek göndererek isterken:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Merhaba yanıt hello JSON nesnesi aşağıdaki gibi görünür:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Merhaba `profile_info` hello uygulamaya - kendi görünen ad, ad, Soyadı, e-posta adresi, tanımlayıcı ve benzeri oturum açan hello kullanıcı hakkındaki bilgileri yer alan değeri.  Öncelikle, hello `profile_info` belirteç önbelleğe alma işlemi için kullanılan ve nedeniyle görüntüler.

Biz şimdi hello kaldırma `profile_info` değer – ancak endişelenmeyin, biz, bu bilgileri toodevelopers biraz farklı bir yerde sağlanmaktadır.  Yerine `profile_info`, hello v2.0 uç şimdi döndürecektir bir `id_token` her belirteci yanıt:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Kod çözme ve hello id_token ayrıştırılamadı tooretrieve hello profile_info alınan aynı bilgileri.  Merhaba id_token bir JSON Web Token (JWT), Openıd Connect tarafından belirtilen içeriğiyle ' dir.  Merhaba bunu kodu çok benzer olmalıdır – tooextract hello Orta yeterlidir segment (Merhaba gövde) hello id_token base64 ve kod çözme tooaccess hello JSON nesnesi içinde.

Merhaba sonraki iki hafta ya da Merhaba, uygulama tooretrieve hello kullanıcı bilgilerinizin kodu `id_token` veya `profile_info`; hangisi mevcuttur.  Merhaba değişiklik yapıldığında bu şekilde, uygulamanızı sorunsuz bir şekilde hello geçiş işleyebilir `profile_info` çok`id_token` kesinti olmadan.

> [!IMPORTANT]
> **İşinizi: uygulamanızı hello hello varlığını bağlı değildir emin olun `profile_info` değeri.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>İd_token_expires_in kaldırma
Benzer çok`profile_info`, biz de hello kaldırma `id_token_expires_in` yanıtlardan parametresi.  Daha önce hello v2.0 uç noktası için bir değer döndürmesi `id_token_expires_in` her id_token yanıtta, örneğin bir authorize yanıt yanı sıra:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

Ya da belirteç yanıtı:

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Merhaba `id_token_expires_in` değeri hello hello id_token kalması için geçerli saniye sayısını belirtmek.  Şimdi, biz hello kaldırıyorsunuz `id_token_expires_in` tamamen değeri.  Bunun yerine, hello Openıd Connect standart kullanabilir `nbf` ve `exp` bir id_token tooexamine hello geçerliliğini talepleri.  Merhaba bkz [v2.0 belirteç başvurusu](active-directory-v2-tokens.md) bu talepler hakkında daha fazla bilgi için.

> [!IMPORTANT]
> **İşinizi: uygulamanızı hello hello varlığını bağlı değildir emin olun `id_token_expires_in` değeri.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Kapsam tarafından döndürülen hello talep değiştirme openıd =
Bu değişiklik hello en önemli – aslında olacaktır, hello v2.0 uç noktası kullanan neredeyse her uygulama etkiler.  Hello kullanarak birçok uygulamaları gönderme istekleri toohello v2.0 uç `openid` gibi kapsam:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Bugün, ne zaman hello kullanıcı verir hello onaylarının `openid` kapsamı, uygulamanızı alır bol miktarda hello kullanıcı hakkındaki bilgileri id_token kaynaklanan hello.  Bu talep adlarıyla, tercih edilen kullanıcı adı, e-posta adresi, nesne kimliği ve daha fazla bilgi içerebilir.

Bu güncelleştirme, biz hello bilgileri o hello değiştiriyorsunuz `openid` kapsam, uygulama erişimini, toobetter comform hello belirtimi Openıd Connect ile ortaya koymaktadır.  Merhaba `openid` kapsam yalnızca uygulama toosign hello kullanıcınız izin ve uygulamaya özgü tanımlayıcıyı hello kullanıcı için hello alırsınız `sub` hello id_token talep.  bir id_token talepleri yalnızca hello ile Merhaba `openid` verilen kapsam herhangi bir kişisel bilgi yoktur olacaktır.  Örnek id_token talep şunlardır:

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Uygulamanızda hello kullanıcı hakkında tooobtain kişisel bilgileri (PII) istiyorsanız, uygulamanızı toorequest hello kullanıcıdan ek izinler gerekir.  İki yeni kapsamlar için destek hello Openıd Connect spec – hello sunuyoruz `email` ve `profile` toodo şekilde izin kapsamları –.

* Merhaba `email` kapsamı çok basit –, uygulama erişim toohello kullanıcının birincil e-posta adresi hello aracılığıyla verir `email` hello id_token talep.  Bu hello Not `email` talep her zaman olmayacak id_tokens içinde mevcut – yalnızca hello kullanıcının profilindeki varsa dahil edilir.
* Merhaba `profile` nesne kimliği kapsam ortaya koymaktadır, uygulama erişim tooall hello kullanıcı – kendi adı, tercih edilen kullanıcı adı, hakkındaki diğer temel bilgileri ve benzeri.

Toocode bu sayede uygulamanız açığa en az bir şekilde – hello kullanıcı uygulamanızı işini toodo gerektirdiği bilgiler yalnızca hello kümesi için sorabilirsiniz.  Uygulamanız şu anda alıyor kullanıcı bilgilerini hello kümesini alma toocontinue istiyorsanız, tüm üç kapsamlar yetkilendirme isteklerinizi içermelidir:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

Uygulamanızı hello gönderme başlayabilirsiniz `email` ve `profile` kapsamları hemen ve hello v2.0 uç bu iki kapsamları kabul ve gerektiği şekilde kullanıcıların izinleri isteyen başlayın.  Bununla birlikte, hello değişikliği hello hello yorumu içinde `openid` kapsamı değil kazanacak için birkaç hafta.

> [!IMPORTANT]
> **İşinizi: hello eklemek `profile` ve `email` uygulamanızı hello kullanıcı hakkındaki bilgileri gerektiriyorsa kapsamları.**  ADAL bu izinlerin ikisini de isteklerinde varsayılan olarak dahil edeceğini unutmayın. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Merhaba veren eğik kaldırılıyor.
Daha önce belirteçleri hello v2.0 uç noktasından görünür hello veren değeriyle hello form sürdü

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Merhaba GUID hello Tenantıd hello belirteç hello Azure AD Kiracı olduğu.  Bu değişikliklerle hello veren değeri olur

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

Her iki simge ve hello Openıd Connect bulma belge.

> [!IMPORTANT]
> **İşinizi: uygulamanızı veren doğrulama sırasında hello veren değeriyle hem ile hem de eğik olmadan kabul ettiğinden emin olun.**
> 
> 

## <a name="why-change"></a>Neden değişiyor?
Bu değişiklikler tanıtımı için birincil motivasyon hello toobe hello standart belirtimi Openıd Connect ile uyumlu olur.  Openıd Connect uyumlu olma yoluyla Microsoft Identity Hizmetleri ve diğer kimlik hizmetlerle hello sektörünün tümleştirme arasındaki farklar toominimize umuyoruz.  Tooenable geliştiriciler toouse kendi sık kullanılan açık kaynak kimlik doğrulama kitaplıkları tooalter hello kitaplıkları tooaccommodate Microsoft farklar gerek kalmadan istiyoruz.

## <a name="what-can-you-do"></a>Ne yapabilirsiniz?
Bugünden itibaren tüm yukarıda açıklanan hello değişiklikleri yapma başlayabilirsiniz.  Hemen yapmanız gerekir:

1. **Merhaba tüm bağımlılıkları kaldırın `x5t` Üstbilgi parametresi.**
2. **Merhaba geçiş işleyebilmesini `profile_info` çok`id_token` belirteci yanıtlarındaki.**
3. **Merhaba tüm bağımlılıkları kaldırın `id_token_expires_in` yanıt parametresi.**
4. **Merhaba eklemek `profile` ve `email` uygulamanızı temel kullanıcı bilgilerini gerekiyorsa kapsamları tooyour uygulama.**
5. **Hem ile hem de eğik olmadan belirteçleri veren değerleri kabul edin.**

Bizim [v2.0 protokolü belgeleri](active-directory-v2-protocols.md) kodunuzu güncelleştirin yardımcı olacak başvuru olarak kullanabilir şekilde güncelleştirilmiş tooreflect bu değişiklikler, zaten.

Merhaba değişiklikleri hello kapsamını herhangi başka bir sorunuz varsa, lütfen ücretsiz tooreach hissedilmesini çıkış Twitter'da toous @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>Protokol değişiklikleri sıklığını?
Biz toohello kimlik doğrulama protokolleri tüm daha fazla kesme değiştirir öngörüyor musunuz.  İstediğiniz zaman tekrar yakında bu tür bir güncelleştirme işlemi üzerinden toogo olmayacaktır böylece Biz bu değişiklikleri bir yayın alanına bilerek paketleme.  Elbette, biz tooadd özellikleri toohello devam edecek özelliklerden yararlanabilirsiniz v2.0 kimlik doğrulama hizmeti Yakınsanan, ancak bu değişiklikleri ADDITIVE ve kod varolan sonu olması gerekir.

Son olarak, hello Önizleme dönemi boyunca şeyler çalışırken için teşekkür ederiz toosay isteriz.  Merhaba Öngörüler ve bizim erken Benimseyenler deneyimlerini bugüne kadarki çok atanmış olması ve tooshare görüşlerini ve fikriniz devam edeceğiz umuyoruz.

Mutluluk kodlama!

Merhaba Microsoft Identity bölme

