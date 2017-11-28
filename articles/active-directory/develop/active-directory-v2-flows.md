---
title: "Azure Active Directory v2.0 uç noktası için uygulama türleri | Microsoft Docs"
description: "Uygulamalar ve Azure Active Directory v2.0 uç noktası tarafından desteklenen senaryoları türleri."
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
ms.openlocfilehash: 9d59e7f0e8f326c40be86e199d7712f6c565cc13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="722c4-103">Azure Active Directory v2.0 uç noktası için uygulama türleri</span><span class="sxs-lookup"><span data-stu-id="722c4-103">App types for the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="722c4-104">Azure Active Directory (Azure AD) v2.0 uç tümünün endüstri standardı protokollerine dayalı modern uygulama mimarilerinin çeşitli kimlik doğrulamasını destekliyor [OAuth 2.0 veya Openıd Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="722c4-105">Bu makalede, tercih edilen dilden veya platformdan bağımsız olarak Azure AD v2.0 kullanarak oluşturabileceğiniz uygulama türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="722c4-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="722c4-106">Bu makaledeki bilgileri, önce üst düzey senaryoları anlamanıza yardımcı olmak için tasarlanmış [kodu ile çalışma başlangıç](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="722c4-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="722c4-107">V2.0 uç noktası, tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="722c4-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="722c4-108">V2.0 uç kullanması gerekip gerekmediğini belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="the-basics"></a><span data-ttu-id="722c4-109">Temel bilgiler</span><span class="sxs-lookup"><span data-stu-id="722c4-109">The basics</span></span>
<span data-ttu-id="722c4-110">V2.0 uç kullanan her bir uygulama kaydettirmelisiniz [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="722c4-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="722c4-111">Uygulama kayıt işlemi toplar ve uygulamanız için bu değerleri atar:</span><span class="sxs-lookup"><span data-stu-id="722c4-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="722c4-112">Bir **uygulama kimliği** uygulamanızı benzersiz olarak tanımlayan</span><span class="sxs-lookup"><span data-stu-id="722c4-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="722c4-113">A **yeniden yönlendirme URI'si** yanıtları uygulamanıza geri yönlendirmek için kullanabileceğiniz</span><span class="sxs-lookup"><span data-stu-id="722c4-113">A **Redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="722c4-114">Birkaç diğer senaryoya özel değerler</span><span class="sxs-lookup"><span data-stu-id="722c4-114">A few other scenario-specific values</span></span>

<span data-ttu-id="722c4-115">Ayrıntılar için bilgi nasıl [uygulama kaydetmeyi](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="722c4-116">Uygulama kaydedildikten sonra uygulamayı Azure AD v2.0 uç noktasına istek göndererek Azure AD ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="722c4-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="722c4-117">Açık kaynak çerçeveler ve bu istekleri ayrıntılarını işlemek kitaplıklar sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="722c4-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="722c4-118">Ayrıca, kimlik doğrulaması mantığı kendiniz Bu uç noktalar isteklerine oluşturarak uygulayacaksınız seçeneğiniz de vardır:</span><span class="sxs-lookup"><span data-stu-id="722c4-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="722c4-119">Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="722c4-119">Web apps</span></span>
<span data-ttu-id="722c4-120">Kullanıcı bir tarayıcıdan erişen web uygulamaları için (.NET, PHP, Java, Ruby, Python, düğüm), kullandığınız [Openıd Connect](active-directory-v2-protocols.md) kullanıcı oturum açma için.</span><span class="sxs-lookup"><span data-stu-id="722c4-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="722c4-121">Openıd Connect web uygulaması kimliği belirteci alır.</span><span class="sxs-lookup"><span data-stu-id="722c4-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="722c4-122">Bir kimliği belirteci, kullanıcının kimliğini doğrular ve talep biçiminde kullanıcı hakkında bilgi sağlayan bir güvenlik belirteci şöyledir:</span><span class="sxs-lookup"><span data-stu-id="722c4-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

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

<span data-ttu-id="722c4-123">Bir uygulama için kullanılabilir talep ve belirteç tüm türleri hakkında bilgi edinebilirsiniz [v2.0 belirteçler başvuru](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="722c4-124">Web sunucusu uygulamalarında oturum açma kimlik doğrulaması akışı aşağıdaki üst düzey adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="722c4-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![Web uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="722c4-126">Kullanıcının kimliğini v2.0 uç noktasından alınan bir ortak imzalama anahtarı ile kimliği belirteci doğrulayarak emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="722c4-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="722c4-127">Sonraki sayfa isteklerinde kullanıcı tanımlamak için kullanılabilecek oturum tanımlama bilgisi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="722c4-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="722c4-128">Bu senaryoyu çalışırken görmek için bizim v2.0 web uygulaması oturum açma kodu örneklerinden birini deneyin [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.</span><span class="sxs-lookup"><span data-stu-id="722c4-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="722c4-129">Basit oturum açma ek olarak, bir REST API'si gibi başka bir web hizmetine erişmek bir web sunucusu uygulaması gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="722c4-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="722c4-130">Bu durumda, web sunucusu uygulaması kullanarak birleşik bir Openıd Connect ve OAuth 2.0 akışı, prosese [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="722c4-131">Bu senaryo hakkında daha fazla bilgi için bilgiyi [web uygulamaları ve Web API ile çalışmaya başlama](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="722c4-132">Web API'leri</span><span class="sxs-lookup"><span data-stu-id="722c4-132">Web APIs</span></span>
<span data-ttu-id="722c4-133">Uygulamanızın RESTful Web API'si gibi web hizmetlerini güvence altına alma v2.0 uç noktası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="722c4-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="722c4-134">Kimlik belirteçlerini ve oturum tanımlama bilgileri yerine, bir Web API, verilerin güvenliğini sağlamak için ve gelen isteklerin kimliğini doğrulamak için bir OAuth 2.0 erişim belirteci kullanır.</span><span class="sxs-lookup"><span data-stu-id="722c4-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="722c4-135">Bir Web API'si çağıran bir erişim belirteci bu gibi bir HTTP isteğinin yetkilendirme üst ekler:</span><span class="sxs-lookup"><span data-stu-id="722c4-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="722c4-136">Web API API çağıranının kimliğini doğrulamak ve erişim belirteçte kodlanmış taleplere çağıran hakkında bilgi ayıklamak için erişim belirtecini kullanır.</span><span class="sxs-lookup"><span data-stu-id="722c4-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="722c4-137">Bir uygulama için kullanılabilir talep ve belirteç tüm türleri hakkında bilgi edinmek için [v2.0 belirteçler başvuru](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="722c4-138">Bir Web API kullanıcıların kabul veya belirli işlevleri veya veri yetersiz izinler olarak da bilinen göstererek opt güç verebilirsiniz [kapsamları](active-directory-v2-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="722c4-139">Bir kapsam için izin almak üzere bir arama uygulaması için kullanıcı akışı sırasında kapsama onaylaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="722c4-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="722c4-140">V2.0 uç noktası kullanıcı için izin ister ve sonra Web API alan tüm erişim belirteçleri izinleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="722c4-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="722c4-141">Web API her çağrıda alır ve yetkilendirme denetimleri gerçekleştirir erişim belirteci doğrular.</span><span class="sxs-lookup"><span data-stu-id="722c4-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="722c4-142">Bir Web API uygulamaları, web sunucu uygulamaları, masaüstü ve mobil uygulamalar, tek sayfa uygulamaları, sunucu tarafı deamon'lar ve hatta diğer Web API'leri dahil olmak üzere tüm türlerinden erişim belirteçleri alabilir.</span><span class="sxs-lookup"><span data-stu-id="722c4-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="722c4-143">Bir Web API için üst düzey akışı şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="722c4-143">The high-level flow for a Web API looks like this:</span></span>

![Web API kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="722c4-145">Web API kod örnekleri kullanıma OAuth2 erişim belirteçleri kullanarak Web API'SİNİN güvenliğini öğrenmek için bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.</span><span class="sxs-lookup"><span data-stu-id="722c4-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="722c4-146">Çoğu durumda, web API'leri de Giden istekleri diğer Aşağı Akış Web API'leri Azure Active Directory tarafından güvenlik altına almanız gereken.</span><span class="sxs-lookup"><span data-stu-id="722c4-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="722c4-147">Bunu yapmak için web API'leri, Azure AD yararlanabilir **adına, üzerinde** Giden istekleri kullanılacak başka bir erişim belirteci için gelen bir erişim belirteci Exchange web API'si sağlar akış.</span><span class="sxs-lookup"><span data-stu-id="722c4-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span></span>  <span data-ttu-id="722c4-148">V2.0 uç noktanın akış adına açıklanan [burada ayrıntı](active-directory-v2-protocols-oauth-on-behalf-of.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="722c4-149">Mobil ve yerel uygulamalar</span><span class="sxs-lookup"><span data-stu-id="722c4-149">Mobile and native apps</span></span>
<span data-ttu-id="722c4-150">Mobil ve Masaüstü uygulamaları gibi cihaz yüklü uygulamalar genellikle arka uç hizmetlerine veya verileri depolamak ve bir kullanıcı adına işlevleri gerçekleştirmek Web API'lerine erişmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="722c4-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="722c4-151">Bu uygulamaları oturum açma ve yetkilendirme için arka uç hizmetlerini kullanarak ekleyebilirsiniz [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="722c4-152">Kullanıcı oturum açtığında bu akışta uygulama v2.0 uç noktasından bir yetkilendirme kodu alır.</span><span class="sxs-lookup"><span data-stu-id="722c4-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="722c4-153">Uygulamanın, oturum açan kullanıcı adına arka uç hizmetlerini çağırma izni yetki kodunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="722c4-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="722c4-154">Uygulama arka planda bir OAuth 2.0 erişim belirteci ve bir yenileme belirteci için yetkilendirme kodu değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="722c4-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="722c4-155">Uygulama için Web API HTTP isteklerinde kimlik doğrulaması için erişim belirtecini kullanır ve eski erişim belirteçleri sona erdiğinde, yeni erişim belirteçleri almak için yenileme belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="722c4-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![Yerel uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="722c4-157">Tek sayfa uygulamaları (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="722c4-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="722c4-158">Birçok modern uygulamanın, JavaScript'te öncelikli olarak yazılmış tek sayfa uygulaması ön ucu sahip.</span><span class="sxs-lookup"><span data-stu-id="722c4-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="722c4-159">Sıklıkla AngularJS, Ember.js veya Durandal.js gibi framework kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="722c4-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="722c4-160">Azure AD v2.0 uç kullanarak bu uygulamaları destekler [OAuth 2.0 örtük akışını](active-directory-v2-protocols-implicit.md).</span><span class="sxs-lookup"><span data-stu-id="722c4-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="722c4-161">Bu akışta uygulama belirteçlerini doğrudan v2.0 aldığı herhangi bir sunucudan sunucuya alışverişleri olmadan son noktanın yetkilendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="722c4-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="722c4-162">Tüm kimlik doğrulaması mantığı ve gerçekleştirilen işlemlerin işleme oturumu tamamen ek sayfa yeniden yönlendirmeleri olmadan JavaScript istemci yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="722c4-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![Örtük kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="722c4-164">Bu senaryoyu çalışırken görmek için tek sayfalı uygulama kodu örneklerinden birini deneyin bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümü.</span><span class="sxs-lookup"><span data-stu-id="722c4-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="722c4-165">Arka plan programları ve sunucu tarafı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="722c4-165">Daemons and server-side apps</span></span>
<span data-ttu-id="722c4-166">Uzun süre çalışan işlemler olması veya, bir kullanıcı etkileşimi olmadan çalışan uygulamalar da Web API'leri gibi güvenli kaynaklara erişmek için bir yol gerekir.</span><span class="sxs-lookup"><span data-stu-id="722c4-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="722c4-167">Bu uygulamaları kimlik doğrulaması ve uygulamanın kimliğini kullanarak belirteçleri almak yerine bir kullanıcı kimliğiyle OAuth 2.0 istemci kimlik bilgileri akışının temsilcisi.</span><span class="sxs-lookup"><span data-stu-id="722c4-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="722c4-168">Bu akışta uygulama doğrudan etkileşimde `/token` uç noktaları edinmek için uç nokta:</span><span class="sxs-lookup"><span data-stu-id="722c4-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![Arka plan programı uygulama kimlik doğrulama akışı](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="722c4-170">Arka plan programı uygulamanızı oluşturmak için istemci kimlik bilgileri belgelerine bakın bizim [Başlarken](active-directory-appmodel-v2-overview.md#getting-started) bölümünde veya deneyin bir [.NET örnek uygulaması](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="722c4-170">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
