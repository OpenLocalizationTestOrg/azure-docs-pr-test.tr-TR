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
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a><span data-ttu-id="3a03a-103">Hello Azure Active Directory v2.0 uç noktası için uygulama türleri</span><span class="sxs-lookup"><span data-stu-id="3a03a-103">App types for hello Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="3a03a-104">Hello Azure Active Directory (Azure AD) v2.0 uç noktası kimlik doğrulaması modern uygulama mimarilerinin tümünün endüstri standardı protokollerine dayalı çeşitli destekleyen [OAuth 2.0 veya Openıd Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-104">hello Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="3a03a-105">Bu makalede hello tercih edilen dilden veya platformdan bağımsız olarak Azure AD v2.0 kullanarak oluşturabileceğiniz uygulama türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3a03a-105">This article describes hello types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="3a03a-106">Merhaba bu makaledeki bilgiler olduğundan, önce üst düzey senaryoları anlamanıza tasarlanmış toohelp [hello kodu ile çalışma başlangıç](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="3a03a-106">hello information in this article is designed toohelp you understand high-level scenarios before you [start working with hello code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="3a03a-107">Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="3a03a-107">hello v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="3a03a-108">mı hello v2.0 uç kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-108">toodetermine whether you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="hello-basics"></a><span data-ttu-id="3a03a-109">Merhaba temelleri</span><span class="sxs-lookup"><span data-stu-id="3a03a-109">hello basics</span></span>
<span data-ttu-id="3a03a-110">Hello hello v2.0 uç noktası kullanan her bir uygulama kaydettirmelisiniz [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3a03a-110">You must register each app that uses hello v2.0 endpoint in hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="3a03a-111">Merhaba uygulama kayıt işlemi toplar ve uygulamanız için bu değerleri atar:</span><span class="sxs-lookup"><span data-stu-id="3a03a-111">hello app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="3a03a-112">Bir **uygulama kimliği** uygulamanızı benzersiz olarak tanımlayan</span><span class="sxs-lookup"><span data-stu-id="3a03a-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="3a03a-113">A **yeniden yönlendirme URI'si** toodirect yanıtları geri tooyour uygulaması kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3a03a-113">A **Redirect URI** that you can use toodirect responses back tooyour app</span></span>
* <span data-ttu-id="3a03a-114">Birkaç diğer senaryoya özel değerler</span><span class="sxs-lookup"><span data-stu-id="3a03a-114">A few other scenario-specific values</span></span>

<span data-ttu-id="3a03a-115">Ayrıntılar için nasıl çok öğrenin[uygulama kaydetmeyi](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-115">For details, learn how too[register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="3a03a-116">Merhaba uygulama kaydedildikten sonra hello uygulama isteklerini toohello Azure AD v2.0 uç göndererek Azure AD ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="3a03a-116">After hello app is registered, hello app communicates with Azure AD by sending requests toohello Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="3a03a-117">Açık kaynak çerçeveler ve bu istekleri hello ayrıntılarını işlemek kitaplıklar sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="3a03a-117">We provide open-source frameworks and libraries that handle hello details of these requests.</span></span> <span data-ttu-id="3a03a-118">Ayrıca hello seçeneği tooimplement hello kimlik doğrulaması mantığı kendiniz toothese uç noktaları istekleri oluşturarak vardır:</span><span class="sxs-lookup"><span data-stu-id="3a03a-118">You also have hello option tooimplement hello authentication logic yourself by creating requests toothese endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a><span data-ttu-id="3a03a-119">Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3a03a-119">Web apps</span></span>
<span data-ttu-id="3a03a-120">Bir tarayıcı aracılığıyla kullanıcı erişimleri hello web uygulamaları için (.NET, PHP, Java, Ruby, Python, düğüm), kullandığınız [Openıd Connect](active-directory-v2-protocols.md) kullanıcı oturum açma için.</span><span class="sxs-lookup"><span data-stu-id="3a03a-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that hello user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="3a03a-121">Openıd Connect içinde hello web uygulaması kimliği belirteci alır.</span><span class="sxs-lookup"><span data-stu-id="3a03a-121">In OpenID Connect, hello web app receives an ID token.</span></span> <span data-ttu-id="3a03a-122">Bir kimliği belirteci hello kullanıcının kimliğini doğrular ve talep hello biçiminde hello kullanıcı hakkında bilgi sağlayan bir güvenlik belirteci şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3a03a-122">An ID token is a security token that verifies hello user's identity and provides information about hello user in hello form of claims:</span></span>

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

<span data-ttu-id="3a03a-123">Merhaba kullanılabilir tooan uygulamada olan talepler ve belirteç tüm hello türleri hakkında bilgi edinebilirsiniz [v2.0 belirteçler başvuru](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-123">You can learn about all hello types of tokens and claims that are available tooan app in hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="3a03a-124">Web sunucusu uygulamalarında hello oturum açma kimlik doğrulaması akışı üst düzey adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="3a03a-124">In web server apps, hello sign-in authentication flow takes these high-level steps:</span></span>

![Web uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="3a03a-126">Merhaba v2.0 uç noktasından alınan bir ortak imzalama anahtarı ile Merhaba kimliği belirteci doğrulayarak hello kullanıcının kimliğini emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a03a-126">You can ensure hello user's identity by validating hello ID token with a public signing key that is received from hello v2.0 endpoint.</span></span> <span data-ttu-id="3a03a-127">Sonraki sayfa isteklerinde kullanılan tooidentify hello kullanıcı olabilen bir oturum tanımlama bilgisi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3a03a-127">A session cookie is set, which can be used tooidentify hello user on subsequent page requests.</span></span>

<span data-ttu-id="3a03a-128">toosee eylemi, oturum açma hello web uygulama kodunuzda birini deneyin içinde bu senaryo örnekleri bizim v2.0 [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3a03a-128">toosee this scenario in action, try one of hello web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="3a03a-129">Ayrıca toosimple oturum açma, bir web sunucusu uygulamasının bir REST API'si gibi başka bir web hizmeti tooaccess gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3a03a-129">In addition toosimple sign-in, a web server app might need tooaccess another web service, such as a REST API.</span></span> <span data-ttu-id="3a03a-130">Bu durumda, hello kullanarak hello web sunucusu uygulamasının birleşik bir Openıd Connect ve OAuth 2.0 akışı, prosese [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-130">In this case, hello web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="3a03a-131">Bu senaryo hakkında daha fazla bilgi için bilgiyi [web uygulamaları ve Web API ile çalışmaya başlama](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="3a03a-132">Web API'leri</span><span class="sxs-lookup"><span data-stu-id="3a03a-132">Web APIs</span></span>
<span data-ttu-id="3a03a-133">Merhaba v2.0 uç noktası toosecure web Hizmetleri, uygulamanızın RESTful Web API'si gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a03a-133">You can use hello v2.0 endpoint toosecure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="3a03a-134">Kimlik belirteçlerini ve oturum tanımlama bilgileri yerine, bir Web API bir OAuth 2.0 erişim belirteci toosecure, veri ve tooauthenticate kullanır gelen istekleri.</span><span class="sxs-lookup"><span data-stu-id="3a03a-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token toosecure its data and tooauthenticate incoming requests.</span></span> <span data-ttu-id="3a03a-135">Web API Hello çağıran bir erişim belirteci bu gibi bir HTTP isteğinin hello yetkilendirme üstbilgisinde ekler:</span><span class="sxs-lookup"><span data-stu-id="3a03a-135">hello caller of a Web API appends an access token in hello authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="3a03a-136">Merhaba Web API hello çağrıyı yapandan hello erişim belirteçte kodlanmış taleplere hakkında hello erişim belirteci tooverify hello API çağıranının kimliğini ve tooextract bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a03a-136">hello Web API uses hello access token tooverify hello API caller's identity and tooextract information about hello caller from claims that are encoded in hello access token.</span></span> <span data-ttu-id="3a03a-137">toolearn kullanılabilir tooan uygulamasına talepler ve belirteç tüm hello türleri hakkında bkz hello [v2.0 belirteçler başvuru](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-137">toolearn about all hello types of tokens and claims that are available tooan app, see hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="3a03a-138">Bir Web API kullanıcılar hello güç tooopt verin veya belirli işlevleri veya veri yetersiz izinler olarak da bilinen göstererek opt [kapsamları](active-directory-v2-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-138">A Web API can give users hello power tooopt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="3a03a-139">Bir arama uygulaması tooacquire izin tooa kapsam için bir akışı sırasında toohello kapsam hello kullanıcı onaylaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a03a-139">For a calling app tooacquire permission tooa scope, hello user must consent toohello scope during a flow.</span></span> <span data-ttu-id="3a03a-140">Merhaba v2.0 uç hello kullanıcı izni ister ve Web API alır, hello'da tüm erişim belirteçleri izinleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3a03a-140">hello v2.0 endpoint asks hello user for permission, and then records permissions in all access tokens that hello Web API receives.</span></span> <span data-ttu-id="3a03a-141">Merhaba Web API her çağrıda alır ve yetkilendirme denetimleri gerçekleştirir hello erişim belirteci doğrular.</span><span class="sxs-lookup"><span data-stu-id="3a03a-141">hello Web API validates hello access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="3a03a-142">Bir Web API uygulamaları, web sunucu uygulamaları, masaüstü ve mobil uygulamalar, tek sayfa uygulamaları, sunucu tarafı deamon'lar ve hatta diğer Web API'leri dahil olmak üzere tüm türlerinden erişim belirteçleri alabilir.</span><span class="sxs-lookup"><span data-stu-id="3a03a-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="3a03a-143">Merhaba üst düzey Akış Web API'si şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="3a03a-143">hello high-level flow for a Web API looks like this:</span></span>

![Web API kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="3a03a-145">toosecure OAuth2 erişim belirteçleri, hello Web API kodunda kullanıma kullanarak bir Web API'sini nasıl örnekleri toolearn bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3a03a-145">toolearn how toosecure a Web API by using OAuth2 access tokens, check out hello Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="3a03a-146">Çoğu durumda, web API'leri da aşağı tooother web API'leri Azure Active Directory tarafından güvenli hale getirilmiş toomake Giden istekleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a03a-146">In many cases, web APIs also need toomake outbound requests tooother downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="3a03a-147">toodo bu nedenle, web API'leri, Azure AD yararlanabilir **adına, üzerinde** hello web API tooexchange giden isteklerinde kullanılan başka bir erişim belirteci toobe için gelen bir erişim belirteci verir akış.</span><span class="sxs-lookup"><span data-stu-id="3a03a-147">toodo so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows hello web API tooexchange an incoming access token for another access token toobe used in outbound requests.</span></span>  <span data-ttu-id="3a03a-148">Merhaba v2.0 uç noktanın akış adına açıklanan [burada ayrıntı](active-directory-v2-protocols-oauth-on-behalf-of.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-148">hello v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="3a03a-149">Mobil ve yerel uygulamalar</span><span class="sxs-lookup"><span data-stu-id="3a03a-149">Mobile and native apps</span></span>
<span data-ttu-id="3a03a-150">Mobil ve Masaüstü uygulamaları gibi cihaz yüklü uygulamalar genellikle tooaccess arka uç hizmetlerine veya Web API'leri, verilerini depolamak ve bir kullanıcı adına işlevleri gerçekleştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a03a-150">Device-installed apps, such as mobile and desktop apps, often need tooaccess back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="3a03a-151">Bu uygulamaları hello kullanarak oturum açma ve yetkilendirme tooback uç hizmetlerinin ekleyebilirsiniz [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-151">These apps can add sign-in and authorization tooback-end services by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="3a03a-152">Merhaba kullanıcı oturum açtığında bu akışta hello uygulama hello v2.0 uç noktasından bir yetkilendirme kodu alır.</span><span class="sxs-lookup"><span data-stu-id="3a03a-152">In this flow, hello app receives an authorization code from hello v2.0 endpoint when hello user signs in.</span></span> <span data-ttu-id="3a03a-153">Yetkilendirme kodu temsil hello uygulamanın izni toocall arka uç hizmetlerinin oturum hello kullanıcı adına hello.</span><span class="sxs-lookup"><span data-stu-id="3a03a-153">hello authorization code represents hello app's permission toocall back-end services on behalf of hello user who is signed in.</span></span> <span data-ttu-id="3a03a-154">Merhaba uygulama hello yetkilendirme kodu hello arka planda bir OAuth 2.0 erişim belirteci ve bir yenileme belirteci değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="3a03a-154">hello app can exchange hello authorization code in hello background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="3a03a-155">Merhaba uygulama HTTP isteklerinde hello erişim belirteci tooauthenticate tooWeb API'leri kullanın ve eski erişim belirteçleri sona erdiğinde hello yenileme belirteci tooget yeni erişim belirteçleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3a03a-155">hello app can use hello access token tooauthenticate tooWeb APIs in HTTP requests, and use hello refresh token tooget new access tokens when older access tokens expire.</span></span>

![Yerel uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="3a03a-157">Tek sayfa uygulamaları (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="3a03a-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="3a03a-158">Birçok modern uygulamanın, JavaScript'te öncelikli olarak yazılmış tek sayfa uygulaması ön ucu sahip.</span><span class="sxs-lookup"><span data-stu-id="3a03a-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="3a03a-159">Sıklıkla AngularJS, Ember.js veya Durandal.js gibi framework kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="3a03a-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="3a03a-160">Hello Azure AD v2.0 uç hello kullanarak bu uygulamaları destekler [OAuth 2.0 örtük akışını](active-directory-v2-protocols-implicit.md).</span><span class="sxs-lookup"><span data-stu-id="3a03a-160">hello Azure AD v2.0 endpoint supports these apps by using hello [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="3a03a-161">Bu akışta hello uygulama belirteçlerini doğrudan hello alır v2.0 uç noktası, herhangi bir sunucudan sunucuya alışverişleri olmadan yetkilendirmek.</span><span class="sxs-lookup"><span data-stu-id="3a03a-161">In this flow, hello app receives tokens directly from hello v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="3a03a-162">Tüm kimlik doğrulaması mantığı ve gerçekleştirilen işlemlerin işleme oturumu tamamen ek sayfa yeniden yönlendirmeleri olmadan hello JavaScript istemci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="3a03a-162">All authentication logic and session handling takes place entirely in hello JavaScript client, without extra page redirects.</span></span>

![Örtük kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="3a03a-164">toosee eylem, bu senaryoda hello tek sayfalı uygulama kodu örneklerinden birini deneyin bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3a03a-164">toosee this scenario in action, try one of hello single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="3a03a-165">Arka plan programları ve sunucu tarafı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="3a03a-165">Daemons and server-side apps</span></span>
<span data-ttu-id="3a03a-166">Uzun süre çalışan işlemler olması veya, bir kullanıcı etkileşimi olmadan çalışan uygulamalar da Web API'leri gibi kaynaklar tooaccess güvenli bir yol gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a03a-166">Apps that have long-running processes or that operate without interaction with a user also need a way tooaccess secured resources, such as Web APIs.</span></span> <span data-ttu-id="3a03a-167">Bu uygulamaları kimlik doğrulaması ve hello uygulamanın kimliğini kullanarak belirteçleri almak yerine bir kullanıcı kimliğiyle hello OAuth 2.0 istemci kimlik bilgileri akışının temsilcisi.</span><span class="sxs-lookup"><span data-stu-id="3a03a-167">These apps can authenticate and get tokens by using hello app's identity, rather than a user's delegated identity, with hello OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="3a03a-168">Bu akışta hello uygulama hello ile doğrudan etkileşim `/token` uç nokta tooobtain uç noktalar:</span><span class="sxs-lookup"><span data-stu-id="3a03a-168">In this flow, hello app interacts directly with hello `/token` endpoint tooobtain endpoints:</span></span>

![Arka plan programı uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="3a03a-170">toobuild bir arka plan programı uygulaması bkz hello istemci kimlik bilgileri belgelerinde bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümünde veya deneyin bir [.NET örnek uygulaması](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="3a03a-170">toobuild a daemon app, see hello client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
