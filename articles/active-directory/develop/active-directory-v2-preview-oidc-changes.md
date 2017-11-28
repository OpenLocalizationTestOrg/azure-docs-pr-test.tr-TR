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
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="b777a-103">Önemli güncelleştirmeleri toohello v2.0 kimlik doğrulama protokolleri</span><span class="sxs-lookup"><span data-stu-id="b777a-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="b777a-104">Uyarı geliştiriciler!</span><span class="sxs-lookup"><span data-stu-id="b777a-104">Attention developers!</span></span> <span data-ttu-id="b777a-105">Merhaba sonraki iki hafta biz birkaç güncelleştirmeleri bizim Önizleme dönemi boyunca yazılmış uygulamalar için önemli değişiklikler olduğu anlamına gelebilir tooour v2.0 kimlik doğrulama protokolleri yapacak.</span><span class="sxs-lookup"><span data-stu-id="b777a-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="b777a-106">Kimin bu etkiliyor mu?</span><span class="sxs-lookup"><span data-stu-id="b777a-106">Who does this affect?</span></span>
<span data-ttu-id="b777a-107">Toouse hello v2.0 yazılmış uygulamalar kimlik doğrulama uç noktası Yakınsanan,</span><span class="sxs-lookup"><span data-stu-id="b777a-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="b777a-108">Merhaba v2.0 uç noktası hakkında daha fazla bilgi bulunabilir [burada](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b777a-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="b777a-109">Bizim Openıd Connect veya OAuth web middlewares birini kullanarak doğrudan toohello v2.0 protokol kodlayarak hello v2.0 uç kullanarak bir uygulama oluşturduktan ya da 3 diğer taraf kitaplıklar tooperform kimlik doğrulamasını kullanarak, olmalısınız yapma ve projeleri tootest hazır gerekirse değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b777a-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="b777a-110">Kimin bu etkilemez?</span><span class="sxs-lookup"><span data-stu-id="b777a-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="b777a-111">Merhaba üretim Azure AD kimlik doğrulama uç noktası karşı yazılan tüm uygulamalar</span><span class="sxs-lookup"><span data-stu-id="b777a-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="b777a-112">Bu protokol taş ayarlanır ve herhangi bir değişiklik yaşayan değil.</span><span class="sxs-lookup"><span data-stu-id="b777a-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="b777a-113">Ayrıca, uygulamanızı **yalnızca** bizim ADAL kitaplığı tooperform kimlik doğrulaması kullanan toochange hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="b777a-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="b777a-114">ADAL hello değişiklikleri uygulamanızdan tam korumalı.</span><span class="sxs-lookup"><span data-stu-id="b777a-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="b777a-115">Merhaba değişiklikleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="b777a-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="b777a-116">Merhaba x5t değeri JWT üstbilgileri kaldırma</span><span class="sxs-lookup"><span data-stu-id="b777a-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="b777a-117">Merhaba v2.0 uç hello belirteci hakkında ilgili meta veriler üstbilgi parametreleri bölümüyle içerir JWT belirteçleri yaygın, kullanır.</span><span class="sxs-lookup"><span data-stu-id="b777a-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="b777a-118">Bizim geçerli Jwt'ler birini hello üstbilgisinin kod çözme, aşağıdakine benzer bulur:</span><span class="sxs-lookup"><span data-stu-id="b777a-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="b777a-119">Her iki hello "x5t" ve "çocuk" özelliklerini hello ortak anahtarı burada tanımlayın, kullanılan toovalidate hello belirtecinin imzası hello Openıd Connect meta veri uç noktasından alınan olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b777a-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="b777a-120">Burada yapıyoruz hello değişiklik tooremove hello "x5t" özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="b777a-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="b777a-121">Aynı mekanizmaları toovalidate belirteçler, ancak yalnızca hello "çocuk" özelliği tooretrieve hello doğru ortak anahtar üzerinde belirtilen hello Openıd Connect Protokolü yararlanmalıdır toouse hello devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="b777a-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b777a-122">**İşinizi: uygulamanızı hello x5t değeri hello varlığını bağlı değildir emin olun.**</span><span class="sxs-lookup"><span data-stu-id="b777a-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="b777a-123">Profile_info kaldırma</span><span class="sxs-lookup"><span data-stu-id="b777a-123">Removing profile_info</span></span>
<span data-ttu-id="b777a-124">Daha önce hello v2.0 uç base64 ile kodlanmış JSON nesnesi adı verilen belirteç yanıtları döndürme `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="b777a-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="b777a-125">Bir erişim belirteci hello v2.0 uç noktasından bir istek göndererek isterken:</span><span class="sxs-lookup"><span data-stu-id="b777a-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="b777a-126">Merhaba yanıt hello JSON nesnesi aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b777a-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="b777a-127">Merhaba `profile_info` hello uygulamaya - kendi görünen ad, ad, Soyadı, e-posta adresi, tanımlayıcı ve benzeri oturum açan hello kullanıcı hakkındaki bilgileri yer alan değeri.</span><span class="sxs-lookup"><span data-stu-id="b777a-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="b777a-128">Öncelikle, hello `profile_info` belirteç önbelleğe alma işlemi için kullanılan ve nedeniyle görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b777a-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="b777a-129">Biz şimdi hello kaldırma `profile_info` değer – ancak endişelenmeyin, biz, bu bilgileri toodevelopers biraz farklı bir yerde sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b777a-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="b777a-130">Yerine `profile_info`, hello v2.0 uç şimdi döndürecektir bir `id_token` her belirteci yanıt:</span><span class="sxs-lookup"><span data-stu-id="b777a-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="b777a-131">Kod çözme ve hello id_token ayrıştırılamadı tooretrieve hello profile_info alınan aynı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b777a-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="b777a-132">Merhaba id_token bir JSON Web Token (JWT), Openıd Connect tarafından belirtilen içeriğiyle ' dir.</span><span class="sxs-lookup"><span data-stu-id="b777a-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="b777a-133">Merhaba bunu kodu çok benzer olmalıdır – tooextract hello Orta yeterlidir segment (Merhaba gövde) hello id_token base64 ve kod çözme tooaccess hello JSON nesnesi içinde.</span><span class="sxs-lookup"><span data-stu-id="b777a-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="b777a-134">Merhaba sonraki iki hafta ya da Merhaba, uygulama tooretrieve hello kullanıcı bilgilerinizin kodu `id_token` veya `profile_info`; hangisi mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="b777a-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="b777a-135">Merhaba değişiklik yapıldığında bu şekilde, uygulamanızı sorunsuz bir şekilde hello geçiş işleyebilir `profile_info` çok`id_token` kesinti olmadan.</span><span class="sxs-lookup"><span data-stu-id="b777a-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b777a-136">**İşinizi: uygulamanızı hello hello varlığını bağlı değildir emin olun `profile_info` değeri.**</span><span class="sxs-lookup"><span data-stu-id="b777a-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="b777a-137">İd_token_expires_in kaldırma</span><span class="sxs-lookup"><span data-stu-id="b777a-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="b777a-138">Benzer çok`profile_info`, biz de hello kaldırma `id_token_expires_in` yanıtlardan parametresi.</span><span class="sxs-lookup"><span data-stu-id="b777a-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="b777a-139">Daha önce hello v2.0 uç noktası için bir değer döndürmesi `id_token_expires_in` her id_token yanıtta, örneğin bir authorize yanıt yanı sıra:</span><span class="sxs-lookup"><span data-stu-id="b777a-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="b777a-140">Ya da belirteç yanıtı:</span><span class="sxs-lookup"><span data-stu-id="b777a-140">Or in a token response:</span></span>

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

<span data-ttu-id="b777a-141">Merhaba `id_token_expires_in` değeri hello hello id_token kalması için geçerli saniye sayısını belirtmek.</span><span class="sxs-lookup"><span data-stu-id="b777a-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="b777a-142">Şimdi, biz hello kaldırıyorsunuz `id_token_expires_in` tamamen değeri.</span><span class="sxs-lookup"><span data-stu-id="b777a-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="b777a-143">Bunun yerine, hello Openıd Connect standart kullanabilir `nbf` ve `exp` bir id_token tooexamine hello geçerliliğini talepleri.</span><span class="sxs-lookup"><span data-stu-id="b777a-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="b777a-144">Merhaba bkz [v2.0 belirteç başvurusu](active-directory-v2-tokens.md) bu talepler hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b777a-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b777a-145">**İşinizi: uygulamanızı hello hello varlığını bağlı değildir emin olun `id_token_expires_in` değeri.**</span><span class="sxs-lookup"><span data-stu-id="b777a-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="b777a-146">Kapsam tarafından döndürülen hello talep değiştirme openıd =</span><span class="sxs-lookup"><span data-stu-id="b777a-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="b777a-147">Bu değişiklik hello en önemli – aslında olacaktır, hello v2.0 uç noktası kullanan neredeyse her uygulama etkiler.</span><span class="sxs-lookup"><span data-stu-id="b777a-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="b777a-148">Hello kullanarak birçok uygulamaları gönderme istekleri toohello v2.0 uç `openid` gibi kapsam:</span><span class="sxs-lookup"><span data-stu-id="b777a-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="b777a-149">Bugün, ne zaman hello kullanıcı verir hello onaylarının `openid` kapsamı, uygulamanızı alır bol miktarda hello kullanıcı hakkındaki bilgileri id_token kaynaklanan hello.</span><span class="sxs-lookup"><span data-stu-id="b777a-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="b777a-150">Bu talep adlarıyla, tercih edilen kullanıcı adı, e-posta adresi, nesne kimliği ve daha fazla bilgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b777a-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="b777a-151">Bu güncelleştirme, biz hello bilgileri o hello değiştiriyorsunuz `openid` kapsam, uygulama erişimini, toobetter comform hello belirtimi Openıd Connect ile ortaya koymaktadır.</span><span class="sxs-lookup"><span data-stu-id="b777a-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="b777a-152">Merhaba `openid` kapsam yalnızca uygulama toosign hello kullanıcınız izin ve uygulamaya özgü tanımlayıcıyı hello kullanıcı için hello alırsınız `sub` hello id_token talep.</span><span class="sxs-lookup"><span data-stu-id="b777a-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="b777a-153">bir id_token talepleri yalnızca hello ile Merhaba `openid` verilen kapsam herhangi bir kişisel bilgi yoktur olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b777a-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="b777a-154">Örnek id_token talep şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b777a-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="b777a-155">Uygulamanızda hello kullanıcı hakkında tooobtain kişisel bilgileri (PII) istiyorsanız, uygulamanızı toorequest hello kullanıcıdan ek izinler gerekir.</span><span class="sxs-lookup"><span data-stu-id="b777a-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="b777a-156">İki yeni kapsamlar için destek hello Openıd Connect spec – hello sunuyoruz `email` ve `profile` toodo şekilde izin kapsamları –.</span><span class="sxs-lookup"><span data-stu-id="b777a-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="b777a-157">Merhaba `email` kapsamı çok basit –, uygulama erişim toohello kullanıcının birincil e-posta adresi hello aracılığıyla verir `email` hello id_token talep.</span><span class="sxs-lookup"><span data-stu-id="b777a-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="b777a-158">Bu hello Not `email` talep her zaman olmayacak id_tokens içinde mevcut – yalnızca hello kullanıcının profilindeki varsa dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="b777a-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="b777a-159">Merhaba `profile` nesne kimliği kapsam ortaya koymaktadır, uygulama erişim tooall hello kullanıcı – kendi adı, tercih edilen kullanıcı adı, hakkındaki diğer temel bilgileri ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="b777a-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="b777a-160">Toocode bu sayede uygulamanız açığa en az bir şekilde – hello kullanıcı uygulamanızı işini toodo gerektirdiği bilgiler yalnızca hello kümesi için sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b777a-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="b777a-161">Uygulamanız şu anda alıyor kullanıcı bilgilerini hello kümesini alma toocontinue istiyorsanız, tüm üç kapsamlar yetkilendirme isteklerinizi içermelidir:</span><span class="sxs-lookup"><span data-stu-id="b777a-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="b777a-162">Uygulamanızı hello gönderme başlayabilirsiniz `email` ve `profile` kapsamları hemen ve hello v2.0 uç bu iki kapsamları kabul ve gerektiği şekilde kullanıcıların izinleri isteyen başlayın.</span><span class="sxs-lookup"><span data-stu-id="b777a-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="b777a-163">Bununla birlikte, hello değişikliği hello hello yorumu içinde `openid` kapsamı değil kazanacak için birkaç hafta.</span><span class="sxs-lookup"><span data-stu-id="b777a-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b777a-164">**İşinizi: hello eklemek `profile` ve `email` uygulamanızı hello kullanıcı hakkındaki bilgileri gerektiriyorsa kapsamları.**</span><span class="sxs-lookup"><span data-stu-id="b777a-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="b777a-165">ADAL bu izinlerin ikisini de isteklerinde varsayılan olarak dahil edeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b777a-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="b777a-166">Merhaba veren eğik kaldırılıyor.</span><span class="sxs-lookup"><span data-stu-id="b777a-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="b777a-167">Daha önce belirteçleri hello v2.0 uç noktasından görünür hello veren değeriyle hello form sürdü</span><span class="sxs-lookup"><span data-stu-id="b777a-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="b777a-168">Merhaba GUID hello Tenantıd hello belirteç hello Azure AD Kiracı olduğu.</span><span class="sxs-lookup"><span data-stu-id="b777a-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="b777a-169">Bu değişikliklerle hello veren değeri olur</span><span class="sxs-lookup"><span data-stu-id="b777a-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="b777a-170">Her iki simge ve hello Openıd Connect bulma belge.</span><span class="sxs-lookup"><span data-stu-id="b777a-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b777a-171">**İşinizi: uygulamanızı veren doğrulama sırasında hello veren değeriyle hem ile hem de eğik olmadan kabul ettiğinden emin olun.**</span><span class="sxs-lookup"><span data-stu-id="b777a-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="b777a-172">Neden değişiyor?</span><span class="sxs-lookup"><span data-stu-id="b777a-172">Why change?</span></span>
<span data-ttu-id="b777a-173">Bu değişiklikler tanıtımı için birincil motivasyon hello toobe hello standart belirtimi Openıd Connect ile uyumlu olur.</span><span class="sxs-lookup"><span data-stu-id="b777a-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="b777a-174">Openıd Connect uyumlu olma yoluyla Microsoft Identity Hizmetleri ve diğer kimlik hizmetlerle hello sektörünün tümleştirme arasındaki farklar toominimize umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="b777a-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="b777a-175">Tooenable geliştiriciler toouse kendi sık kullanılan açık kaynak kimlik doğrulama kitaplıkları tooalter hello kitaplıkları tooaccommodate Microsoft farklar gerek kalmadan istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b777a-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="b777a-176">Ne yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="b777a-176">What can you do?</span></span>
<span data-ttu-id="b777a-177">Bugünden itibaren tüm yukarıda açıklanan hello değişiklikleri yapma başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b777a-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="b777a-178">Hemen yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b777a-178">You should immediately:</span></span>

1. <span data-ttu-id="b777a-179">**Merhaba tüm bağımlılıkları kaldırın `x5t` Üstbilgi parametresi.**</span><span class="sxs-lookup"><span data-stu-id="b777a-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="b777a-180">**Merhaba geçiş işleyebilmesini `profile_info` çok`id_token` belirteci yanıtlarındaki.**</span><span class="sxs-lookup"><span data-stu-id="b777a-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="b777a-181">**Merhaba tüm bağımlılıkları kaldırın `id_token_expires_in` yanıt parametresi.**</span><span class="sxs-lookup"><span data-stu-id="b777a-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="b777a-182">**Merhaba eklemek `profile` ve `email` uygulamanızı temel kullanıcı bilgilerini gerekiyorsa kapsamları tooyour uygulama.**</span><span class="sxs-lookup"><span data-stu-id="b777a-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="b777a-183">**Hem ile hem de eğik olmadan belirteçleri veren değerleri kabul edin.**</span><span class="sxs-lookup"><span data-stu-id="b777a-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="b777a-184">Bizim [v2.0 protokolü belgeleri](active-directory-v2-protocols.md) kodunuzu güncelleştirin yardımcı olacak başvuru olarak kullanabilir şekilde güncelleştirilmiş tooreflect bu değişiklikler, zaten.</span><span class="sxs-lookup"><span data-stu-id="b777a-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="b777a-185">Merhaba değişiklikleri hello kapsamını herhangi başka bir sorunuz varsa, lütfen ücretsiz tooreach hissedilmesini çıkış Twitter'da toous @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="b777a-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="b777a-186">Protokol değişiklikleri sıklığını?</span><span class="sxs-lookup"><span data-stu-id="b777a-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="b777a-187">Biz toohello kimlik doğrulama protokolleri tüm daha fazla kesme değiştirir öngörüyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="b777a-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="b777a-188">İstediğiniz zaman tekrar yakında bu tür bir güncelleştirme işlemi üzerinden toogo olmayacaktır böylece Biz bu değişiklikleri bir yayın alanına bilerek paketleme.</span><span class="sxs-lookup"><span data-stu-id="b777a-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="b777a-189">Elbette, biz tooadd özellikleri toohello devam edecek özelliklerden yararlanabilirsiniz v2.0 kimlik doğrulama hizmeti Yakınsanan, ancak bu değişiklikleri ADDITIVE ve kod varolan sonu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b777a-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="b777a-190">Son olarak, hello Önizleme dönemi boyunca şeyler çalışırken için teşekkür ederiz toosay isteriz.</span><span class="sxs-lookup"><span data-stu-id="b777a-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="b777a-191">Merhaba Öngörüler ve bizim erken Benimseyenler deneyimlerini bugüne kadarki çok atanmış olması ve tooshare görüşlerini ve fikriniz devam edeceğiz umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="b777a-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="b777a-192">Mutluluk kodlama!</span><span class="sxs-lookup"><span data-stu-id="b777a-192">Happy coding!</span></span>

<span data-ttu-id="b777a-193">Merhaba Microsoft Identity bölme</span><span class="sxs-lookup"><span data-stu-id="b777a-193">hello Microsoft Identity Division</span></span>

