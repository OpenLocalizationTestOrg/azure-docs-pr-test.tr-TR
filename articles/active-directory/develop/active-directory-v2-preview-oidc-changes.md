---
title: "Azure AD v2.0 uç noktasına değişiklikleri | Microsoft Docs"
description: "Uygulama modeli v2.0 Genel Önizleme protokolleri yapılan değişikliklerin bir açıklaması."
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
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="04c12-103">Önemli güncelleştirmeleri v2.0 kimlik doğrulama protokolleri</span><span class="sxs-lookup"><span data-stu-id="04c12-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="04c12-104">Uyarı geliştiriciler!</span><span class="sxs-lookup"><span data-stu-id="04c12-104">Attention developers!</span></span> <span data-ttu-id="04c12-105">Sonraki iki hafta boyunca size birkaç güncelleştirmeleri bizim Önizleme dönemi boyunca yazılmış uygulamalar için önemli değişiklikler olduğu anlamına gelebilir bizim v2.0 kimlik doğrulama protokolleri için yapacak.</span><span class="sxs-lookup"><span data-stu-id="04c12-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="04c12-106">Kimin bu etkiliyor mu?</span><span class="sxs-lookup"><span data-stu-id="04c12-106">Who does this affect?</span></span>
<span data-ttu-id="04c12-107">V2.0 kullanmak için yazılmış olan tüm uygulamaların kimlik doğrulama uç noktası Yakınsanan,</span><span class="sxs-lookup"><span data-stu-id="04c12-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="04c12-108">V2.0 uç noktası hakkında daha fazla bilgi bulunabilir [burada](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04c12-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="04c12-109">V2.0 uç noktası doğrudan v2.0 protokol kodlayarak kullanarak bir uygulama oluşturduysanız bizim Openıd Connect veya OAuth web middlewares birini kullanarak veya kimlik doğrulaması gerçekleştirmek için 3 diğer taraf kitaplıklar kullanılarak, projelerinizi test ve değişiklikler yapmak için hazırlıklı olmalıdır Gerekirse.</span><span class="sxs-lookup"><span data-stu-id="04c12-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="04c12-110">Kimin bu etkilemez?</span><span class="sxs-lookup"><span data-stu-id="04c12-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="04c12-111">Üretim Azure AD kimlik doğrulama uç noktası karşı yazılan tüm uygulamalar</span><span class="sxs-lookup"><span data-stu-id="04c12-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="04c12-112">Bu protokol taş ayarlanır ve herhangi bir değişiklik yaşayan değil.</span><span class="sxs-lookup"><span data-stu-id="04c12-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="04c12-113">Ayrıca, uygulamanızı **yalnızca** kimlik doğrulaması gerçekleştirmek için bizim ADAL kitaplığını kullanır değişikliği gerekmez.</span><span class="sxs-lookup"><span data-stu-id="04c12-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="04c12-114">ADAL değişiklikleri uygulamanızdan tam korumalı.</span><span class="sxs-lookup"><span data-stu-id="04c12-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="04c12-115">Değişiklikleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="04c12-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="04c12-116">JWT üstbilgileri x5t değeri kaldırma</span><span class="sxs-lookup"><span data-stu-id="04c12-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="04c12-117">V2.0 uç belirteç hakkında ilgili meta veriler üstbilgi parametreleri bölümüyle içerir JWT belirteçleri yaygın, kullanır.</span><span class="sxs-lookup"><span data-stu-id="04c12-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="04c12-118">Bizim geçerli Jwt'ler birini üstbilgisi kod çözme, aşağıdakine benzer bulur:</span><span class="sxs-lookup"><span data-stu-id="04c12-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="04c12-119">Burada "x5t" ve "anlaşmalı" özellikleri Openıd Connect meta veri uç noktasından alınan olarak belirtecin imzayı doğrulamak için kullanılacak ortak anahtarı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="04c12-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="04c12-120">Burada yapıyoruz "x5t" özelliği kaldırmak için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="04c12-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="04c12-121">Belirteçleri doğrulamak için mekanizmalarının aynısını kullanmaya devam edebilir, ancak doğru ortak anahtar Openıd Connect Protokolü belirtilen olarak almak için yalnızca "anlaşmalı" özelliğini yararlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="04c12-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="04c12-122">**İşinizi: uygulamanızı x5t değeri varlığını bağlı değildir emin olun.**</span><span class="sxs-lookup"><span data-stu-id="04c12-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="04c12-123">Profile_info kaldırma</span><span class="sxs-lookup"><span data-stu-id="04c12-123">Removing profile_info</span></span>
<span data-ttu-id="04c12-124">Daha önce v2.0 uç noktası bir base64 ile kodlanmış JSON nesnesi adı verilen belirteç yanıtları döndürme edilmiş `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="04c12-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="04c12-125">Bir erişim belirteci v2.0 uç noktasından bir istek göndererek isterken:</span><span class="sxs-lookup"><span data-stu-id="04c12-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="04c12-126">Yanıt aşağıdaki JSON nesnesi gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="04c12-126">The response would look like the following JSON object:</span></span>

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

<span data-ttu-id="04c12-127">`profile_info` Uygulamaya - kendi görünen ad, ad, Soyadı, e-posta adresi, tanımlayıcı ve benzeri oturum açan kullanıcı bilgilerini bulunan değer.</span><span class="sxs-lookup"><span data-stu-id="04c12-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="04c12-128">Öncelikle, `profile_info` belirteç önbelleğe alma işlemi için kullanılan ve nedeniyle görüntüler.</span><span class="sxs-lookup"><span data-stu-id="04c12-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="04c12-129">Biz şimdi kaldırma `profile_info` değer – ancak endişelenmeyin, biz yine bu bilgiler biraz farklı bir yerde geliştiricilere sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="04c12-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="04c12-130">Yerine `profile_info`, v2.0 uç şimdi döndürülecek bir `id_token` her belirteci yanıt:</span><span class="sxs-lookup"><span data-stu-id="04c12-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="04c12-131">Kod çözme ve profile_info alınan aynı bilgileri almak için id_token ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="04c12-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="04c12-132">İd_token bir JSON Web Token (JWT), Openıd Connect tarafından belirtilen içeriğiyle ' dir.</span><span class="sxs-lookup"><span data-stu-id="04c12-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="04c12-133">Bunu yapmak için kod kadar çok benzer olmalıdır – id_token Orta segment (gövde) ayıklamak yeterlidir ve base64 JSON nesnesi içinde erişmek için kod çözme.</span><span class="sxs-lookup"><span data-stu-id="04c12-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="04c12-134">Sonraki iki hafta içinde kullanıcı bilgilerini herhangi birinden almak için uygulamanızı kod `id_token` veya `profile_info`; hangisi mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="04c12-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="04c12-135">Değişiklik yapıldığında bu şekilde, uygulamanızı sorunsuz geçiş işleyebilir `profile_info` için `id_token` kesinti olmadan.</span><span class="sxs-lookup"><span data-stu-id="04c12-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04c12-136">**İşinizi: uygulamanızı varlığını bağlı değildir emin olun `profile_info` değeri.**</span><span class="sxs-lookup"><span data-stu-id="04c12-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="04c12-137">İd_token_expires_in kaldırma</span><span class="sxs-lookup"><span data-stu-id="04c12-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="04c12-138">Benzer şekilde `profile_info`, biz de kaldırma `id_token_expires_in` yanıtlardan parametresi.</span><span class="sxs-lookup"><span data-stu-id="04c12-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="04c12-139">Daha önce v2.0 uç noktası için bir değer döndürmesi `id_token_expires_in` her id_token yanıtta, örneğin bir authorize yanıt yanı sıra:</span><span class="sxs-lookup"><span data-stu-id="04c12-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="04c12-140">Ya da belirteç yanıtı:</span><span class="sxs-lookup"><span data-stu-id="04c12-140">Or in a token response:</span></span>

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

<span data-ttu-id="04c12-141">`id_token_expires_in` Değeri id_token kalması için geçerli saniye sayısını belirtmek.</span><span class="sxs-lookup"><span data-stu-id="04c12-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="04c12-142">Şimdi, biz kaldırıyorsunuz `id_token_expires_in` tamamen değeri.</span><span class="sxs-lookup"><span data-stu-id="04c12-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="04c12-143">Bunun yerine, Openıd Connect standart kullanabilir `nbf` ve `exp` bir id_token geçerliliğini incelemek talep.</span><span class="sxs-lookup"><span data-stu-id="04c12-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="04c12-144">Bkz: [v2.0 belirteç başvurusu](active-directory-v2-tokens.md) bu talepler hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="04c12-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04c12-145">**İşinizi: uygulamanızı varlığını bağlı değildir emin olun `id_token_expires_in` değeri.**</span><span class="sxs-lookup"><span data-stu-id="04c12-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="04c12-146">Kapsam tarafından döndürülen talep değiştirme openıd =</span><span class="sxs-lookup"><span data-stu-id="04c12-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="04c12-147">Bu değişiklik en önemli – aslında, v2.0 uç noktası kullanan neredeyse her uygulama etkiler.</span><span class="sxs-lookup"><span data-stu-id="04c12-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="04c12-148">Birçok uygulama, v2.0 uç noktası için kullanılacak istekleri göndermek `openid` gibi kapsam:</span><span class="sxs-lookup"><span data-stu-id="04c12-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="04c12-149">Bugün, ne zaman kullanıcıya izin verir `openid` kapsam, uygulamanızın elde edilen id_token çok sayıda kullanıcı hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="04c12-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="04c12-150">Bu talep adlarıyla, tercih edilen kullanıcı adı, e-posta adresi, nesne kimliği ve daha fazla bilgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="04c12-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="04c12-151">Bu güncelleştirme, biz bilgileri değiştiriyorsunuz, `openid` kapsam için daha iyi comform Openıd Connect belirtimiyle, uygulama erişimini ortaya koymaktadır.</span><span class="sxs-lookup"><span data-stu-id="04c12-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="04c12-152">`openid` Kapsam yalnızca kullanıcı oturum sağlamak ve kullanıcı için uygulamaya özgü tanımlayıcıyı alma `sub` id_token talep.</span><span class="sxs-lookup"><span data-stu-id="04c12-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="04c12-153">Yalnızca bir id_token Taleplerde `openid` verilen kapsam herhangi bir kişisel bilgi yoktur olacaktır.</span><span class="sxs-lookup"><span data-stu-id="04c12-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="04c12-154">Örnek id_token talep şunlardır:</span><span class="sxs-lookup"><span data-stu-id="04c12-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="04c12-155">Uygulamanızda kullanıcıyla ilgili kişisel bilgileri (PII) elde etmek istiyorsanız, uygulamanızı kullanıcıdan ek izinler istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c12-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="04c12-156">Openıd Connect spec – iki yeni kapsamlar için destek sunuyoruz `email` ve `profile` , bunu yapmak izin kapsamları –.</span><span class="sxs-lookup"><span data-stu-id="04c12-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="04c12-157">`email` Kapsamı çok basit – kullanıcının birincil e-posta adresi uygulama erişiminizi sağlayan `email` id_token talep.</span><span class="sxs-lookup"><span data-stu-id="04c12-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="04c12-158">Unutmayın `email` talep her zaman olmayacak id_tokens içinde mevcut – yalnızca kullanıcının profilinde varsa dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="04c12-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="04c12-159">`profile` Kapsam ortaya koymaktadır tüm diğer ilgili temel bilgileri kendi adı, tercih edilen kullanıcı adı, bir kullanıcının, uygulama erişimini nesne kimliği ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="04c12-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="04c12-160">Bu sayede uygulamanız açığa en az bir şekilde kod – yalnızca uygulamanızı işini yapmak için gerektirdiği bilgiler kümesi için kullanıcıya sor.</span><span class="sxs-lookup"><span data-stu-id="04c12-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="04c12-161">Kümesini uygulamanız şu anda alıyor kullanıcı bilgileri alma devam etmek istiyorsanız, tüm üç kapsamlar yetkilendirme isteklerinizi içermelidir:</span><span class="sxs-lookup"><span data-stu-id="04c12-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="04c12-162">Uygulamanızı göndermeye başlamak `email` ve `profile` hemen kapsamlar ve v2.0 uç noktası bu iki kapsamları kabul ve gerektiği şekilde kullanıcıların izinleri isteyen başlamak.</span><span class="sxs-lookup"><span data-stu-id="04c12-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="04c12-163">Ancak, yorumu değişikliği `openid` kapsamı değil kazanacak için birkaç hafta.</span><span class="sxs-lookup"><span data-stu-id="04c12-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04c12-164">**İşinizi: eklemek `profile` ve `email` uygulamanızı kullanıcı hakkındaki bilgileri gerektiriyorsa kapsamları.**</span><span class="sxs-lookup"><span data-stu-id="04c12-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="04c12-165">ADAL bu izinlerin ikisini de isteklerinde varsayılan olarak dahil edeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04c12-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="04c12-166">Sondaki eğik çizgi veren kaldırılıyor.</span><span class="sxs-lookup"><span data-stu-id="04c12-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="04c12-167">Daha önce v2.0 uç noktasından belirteçleri görünen veren değeri form sürdü</span><span class="sxs-lookup"><span data-stu-id="04c12-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="04c12-168">GUID, belirtecin Azure AD kiracısı Tenantıd olduğu.</span><span class="sxs-lookup"><span data-stu-id="04c12-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="04c12-169">Bu değişikliklerle veren değeri olur</span><span class="sxs-lookup"><span data-stu-id="04c12-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="04c12-170">Her iki simge ve Openıd Connect bulma belge.</span><span class="sxs-lookup"><span data-stu-id="04c12-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04c12-171">**İşinizi: uygulamanızı veren doğrulama sırasında hem ile hem de eğik olmadan veren değeri kabul ettiğinden emin olun.**</span><span class="sxs-lookup"><span data-stu-id="04c12-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="04c12-172">Neden değişiyor?</span><span class="sxs-lookup"><span data-stu-id="04c12-172">Why change?</span></span>
<span data-ttu-id="04c12-173">Bu değişiklikler tanıtımı için birincil motivasyon Openıd Connect standart belirtimi ile uyumlu olacak.</span><span class="sxs-lookup"><span data-stu-id="04c12-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="04c12-174">Openıd Connect uyumlu olma yoluyla Microsoft Identity hizmetleriyle ve diğer endüstri kimlik Hizmetleri ile tümleştirme arasındaki farklar en aza indirmek umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="04c12-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="04c12-175">Microsoft farklara uyum sağlamak için kitaplıkları değiştirmek zorunda kalmadan kendi sık kullanılan açık kaynak kimlik doğrulama kitaplıkları kullanabilirsiniz, geliştiricilerin istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="04c12-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="04c12-176">Ne yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="04c12-176">What can you do?</span></span>
<span data-ttu-id="04c12-177">Bugün itibariyle, yukarıda açıklanan tüm değişiklikleri yapma başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04c12-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="04c12-178">Hemen yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="04c12-178">You should immediately:</span></span>

1. <span data-ttu-id="04c12-179">**Bağımlılıkları kaldırmak `x5t` Üstbilgi parametresi.**</span><span class="sxs-lookup"><span data-stu-id="04c12-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="04c12-180">**Geçiş işleyebilmesini `profile_info` için `id_token` belirteci yanıtlarındaki.**</span><span class="sxs-lookup"><span data-stu-id="04c12-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="04c12-181">**Bağımlılıkları kaldırmak `id_token_expires_in` yanıt parametresi.**</span><span class="sxs-lookup"><span data-stu-id="04c12-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="04c12-182">**Ekleme `profile` ve `email` uygulamanızı temel kullanıcı bilgileri gerektiriyorsa, uygulamanızın kapsamları.**</span><span class="sxs-lookup"><span data-stu-id="04c12-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="04c12-183">**Hem ile hem de eğik olmadan belirteçleri veren değerleri kabul edin.**</span><span class="sxs-lookup"><span data-stu-id="04c12-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="04c12-184">Bizim [v2.0 protokolü belgeleri](active-directory-v2-protocols.md) zaten kodunuzu güncelleştirin yardımcı olacak başvuru olarak kullanabilir şekilde bu değişiklikleri yansıtacak şekilde güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="04c12-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="04c12-185">Değişiklikleri kapsamını herhangi bir sorunuz varsa, lütfen Twitter'da Bize Ulaşın çekinmeyin @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="04c12-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="04c12-186">Protokol değişiklikleri sıklığını?</span><span class="sxs-lookup"><span data-stu-id="04c12-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="04c12-187">Şu kimlik doğrulama protokolleri tüm daha fazla kesme değiştirir öngörüyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="04c12-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="04c12-188">İstediğiniz zaman tekrar yakında güncelleştirme işlemini bu tür gitmek zorunda kalmazsınız böylece Biz bu değişiklikleri bir yayın alanına bilerek paketleme.</span><span class="sxs-lookup"><span data-stu-id="04c12-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="04c12-189">Elbette, avantajlarından yararlanmak yakınsanmış v2.0 kimlik doğrulama hizmeti özellikleri eklemek devam, ancak bu değişiklikleri ADDITIVE ve kod varolan sonu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="04c12-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="04c12-190">Son olarak, Önizleme dönemi boyunca şeyler çalışırken için teşekkür ederiz söylemek isteriz.</span><span class="sxs-lookup"><span data-stu-id="04c12-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="04c12-191">Öngörüler ve bizim erken Benimseyenler deneyimlerini bugüne kadarki çok atanmış olması ve sizin görüşlerini paylaşın devam edeceğiz umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="04c12-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="04c12-192">Mutluluk kodlama!</span><span class="sxs-lookup"><span data-stu-id="04c12-192">Happy coding!</span></span>

<span data-ttu-id="04c12-193">Microsoft Identity bölme</span><span class="sxs-lookup"><span data-stu-id="04c12-193">The Microsoft Identity Division</span></span>

