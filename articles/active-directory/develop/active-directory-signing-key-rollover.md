---
title: "Anahtar geçişi Azure AD'de aaaSigning | Microsoft Docs"
description: "Bu makalede, anahtar geçişi en iyi uygulamaları için Azure Active Directory imzalama hello anlatılmaktadır."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="51507-103">Azure Active Directory'de anahtar geçişi imzalama</span><span class="sxs-lookup"><span data-stu-id="51507-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="51507-104">Bu konuda, Azure Active Directory (Azure AD) toosign güvenlik belirteçlerinde kullanılan hello ortak anahtarları hakkında tooknow gerekenler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="51507-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="51507-105">Bu anahtarları rollover düzenli aralıklarla ve acil bir durumda uzatılabilir hemen önemli toonote olur.</span><span class="sxs-lookup"><span data-stu-id="51507-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="51507-106">Azure AD kullanan tüm uygulamalar, mümkün tooprogrammatically tanıtıcı hello anahtarı geçiş işlemi veya düzenli el ile geçiş işlemi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="51507-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="51507-107">Hello anahtarları iş nasıl tooassess Merhaba rollover tooyour uygulaması etkisini nasıl hello ve nasıl toounderstand okuma devam tooupdate uygulamanızı veya düzenli el ile geçiş işlemi toohandle anahtar geçişi gerekirse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="51507-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="51507-108">Azure AD'de imzalama anahtarlarının genel bakış</span><span class="sxs-lookup"><span data-stu-id="51507-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="51507-109">Azure AD kullanır kendisi ve hello arasında endüstri standartları tooestablish güven üzerine kurulu ortak anahtar şifrelemesi kullanan uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="51507-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="51507-110">Pratikteki, bu yolu izleyerek hello çalışır: Azure AD genel ve özel bir anahtar çiftinden oluşur imzalama bir anahtar kullanır.</span><span class="sxs-lookup"><span data-stu-id="51507-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="51507-111">Azure AD kimlik doğrulaması için kullandığı tooan uygulamada bir kullanıcı oturum açtığında, Azure AD hello kullanıcı hakkındaki bilgileri içeren bir güvenlik belirteci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="51507-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="51507-112">Bu belirteç geri toohello uygulama gönderilmeden önce özel anahtarını kullanarak Azure AD tarafından imzalanır.</span><span class="sxs-lookup"><span data-stu-id="51507-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="51507-113">belirteç hello tooverify geçerli olduğundan ve Azure AD'den gerçekte kaynaklı, Merhaba uygulaması hello kiracının içinde yer alan Azure AD tarafından sunulan hello ortak anahtarı kullanılarak hello belirtecinin imzası doğrulama gerekir [Openıd Connect bulma belge](http://openid.net/specs/openid-connect-discovery-1_0.html) veya SAML/WS-Fed [Federasyon meta veri belgesi](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="51507-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="51507-114">Güvenlik nedeniyle, Azure AD anahtar dökümünü düzenli aralıklarla ve acil bir hello durumda imzalama uzatılabilir hemen.</span><span class="sxs-lookup"><span data-stu-id="51507-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="51507-115">Azure AD ile tümleşir herhangi bir uygulama bir anahtar geçişi olayı Hayır önemli ne sıklıkta oluşabilir toohandle hazırlıklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51507-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="51507-116">Yoktur ve uygulamanızı toouse bir belirteç süresi dolan anahtar tooverify hello imza çalışır hello oturum açma isteği başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="51507-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="51507-117">Her zaman birden fazla geçerli anahtar hello Openıd Connect bulma belge ve hello Federasyon meta veri belgesi mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="51507-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="51507-118">Uygulamanızı hazırlıklı olmalıdır toouse hello anahtarlardan herhangi birine belirtilen hello belgede bir anahtar yakında geri alınması beri başka değişimi olması ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="51507-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="51507-119">Nasıl uygulamanızı etkilenecek varsa tooassess ve onunla ilgili hangi toodo</span><span class="sxs-lookup"><span data-stu-id="51507-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="51507-120">Anahtar geçişi, uygulamanızın nasıl işlediğini uygulama veya hangi kimlik protokolü ve kitaplık kullanıldı hello türü gibi değişkenleri bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="51507-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="51507-121">Aşağıdaki hello bölümler Hello en yaygın uygulama türlerini hello anahtar geçişi tarafından etkilenen ve kılavuzluk nasıl tooupdate uygulama toosupport otomatik geçişi hello veya el ile Merhaba anahtarı güncelleştirme olup olmadığını değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="51507-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="51507-122">Yerel istemci uygulamaları kaynaklara erişme</span><span class="sxs-lookup"><span data-stu-id="51507-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="51507-123">Web uygulamaları / API'leri kaynaklara erişme</span><span class="sxs-lookup"><span data-stu-id="51507-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="51507-124">Web uygulamaları / API'leri kaynakları koruma ve Azure App Services kullanılarak oluşturulmuş</span><span class="sxs-lookup"><span data-stu-id="51507-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="51507-125">Web uygulamaları / .NET OWIN Openıd Connect, WS-Fed veya WindowsAzureActiveDirectoryBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="51507-126">Web uygulamaları / .NET Core Openıd Connect veya JwtBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="51507-127">Web uygulamaları / Node.js passport azure ad modülünü kullanarak kaynakları koruma API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="51507-128">Web uygulamaları / API'leri kaynakları koruma ve Visual Studio 2015 veya Visual Studio 2017 oluşturulmuş</span><span class="sxs-lookup"><span data-stu-id="51507-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="51507-129">Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="51507-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="51507-130">Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="51507-131">Kaynakları koruma ve Visual Studio 2012 ile oluşturulan web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="51507-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="51507-132">Kaynakları koruma ve Windows Identity Foundation'ı kullanarak 2008 o Visual Studio 2010 ile oluşturulan web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="51507-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="51507-133">Web uygulamaları / kaynakları koruma API'leri kullanarak diğer kitaplıkları veya el ile Merhaba hiçbirini uygulama protokolleri desteklenmez</span><span class="sxs-lookup"><span data-stu-id="51507-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="51507-134">Bu kılavuz **değil** için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="51507-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="51507-135">Azure AD uygulama (özel dahil) galerisinden eklenen uygulamalar bakımından toosigning anahtarlarla ayrı yönergeler vardır.</span><span class="sxs-lookup"><span data-stu-id="51507-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="51507-136">Daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="51507-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="51507-137">Uygulama Ara sunucusu üzerinden yayımlanan uygulamalarla anahtarları imzalama hakkında tooworry yoksa şirket içi.</span><span class="sxs-lookup"><span data-stu-id="51507-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="51507-138"><a name="nativeclient"></a>Yerel istemci uygulamaları kaynaklara erişme</span><span class="sxs-lookup"><span data-stu-id="51507-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="51507-139">Yalnızca (yani kaynaklarına erişen uygulamalar</span><span class="sxs-lookup"><span data-stu-id="51507-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="51507-140">Microsoft Graph, KeyVault, Outlook API ve diğer Microsoft APIs) genellikle yalnızca bir belirteç elde ve toohello kaynak sahibi geçirin.</span><span class="sxs-lookup"><span data-stu-id="51507-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="51507-141">O tüm kaynakları koruma değil, hello belirteci incelemek değil ve bu nedenle doğru şekilde imzalanmış tooensure gerekmez.</span><span class="sxs-lookup"><span data-stu-id="51507-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="51507-142">Yerel istemci uygulamaları, masaüstü veya mobil, bu kategoriye ve böylece hello rollover tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="51507-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="51507-143"><a name="webclient"></a>Web uygulamaları / API'leri kaynaklara erişme</span><span class="sxs-lookup"><span data-stu-id="51507-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="51507-144">Yalnızca (yani kaynaklarına erişen uygulamalar</span><span class="sxs-lookup"><span data-stu-id="51507-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="51507-145">Microsoft Graph, KeyVault, Outlook API ve diğer Microsoft APIs) genellikle yalnızca bir belirteç elde ve toohello kaynak sahibi geçirin.</span><span class="sxs-lookup"><span data-stu-id="51507-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="51507-146">O tüm kaynakları koruma değil, hello belirteci incelemek değil ve bu nedenle doğru şekilde imzalanmış tooensure gerekmez.</span><span class="sxs-lookup"><span data-stu-id="51507-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="51507-147">Web uygulamaları ve web hello yalnızca uygulama akışı kullanarak API'leri (istemci kimlik bilgileri / istemci sertifikası), bu kategoriye girer ve bu nedenle hello rollover tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="51507-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="51507-148"><a name="appservices"></a>Web uygulamaları / API'leri kaynakları koruma ve Azure App Services kullanılarak oluşturulmuş</span><span class="sxs-lookup"><span data-stu-id="51507-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="51507-149">Azure uygulama hizmetleri kimlik doğrulama / yetkilendirme (EasyAuth) işlevselliği zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="51507-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="51507-150"><a name="owin"></a>Web uygulamaları / .NET OWIN Openıd Connect, WS-Fed veya WindowsAzureActiveDirectoryBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="51507-151">Uygulamanızı hello .NET OWIN Openıd Connect, WS-Fed veya WindowsAzureActiveDirectoryBearerAuthentication ara yazılımı kullanıyorsanız, zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak içeriyor.</span><span class="sxs-lookup"><span data-stu-id="51507-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="51507-152">Uygulamanız herhangi birini herhangi parçacıkları uygulamanızın haline veya Startup.Auth.cs aşağıdaki hello bakarak kullandığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="51507-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="51507-153"><a name="owincore"></a>Web uygulamaları / .NET Core Openıd Connect veya JwtBearerAuthentication ara yazılımı kullanarak kaynakları koruma API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="51507-154">Uygulamanızı hello .NET Core OWIN Openıd Connect veya JwtBearerAuthentication ara yazılımı kullanıyorsanız, zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak içeriyor.</span><span class="sxs-lookup"><span data-stu-id="51507-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="51507-155">Uygulamanız herhangi birini herhangi parçacıkları uygulamanızın haline veya Startup.Auth.cs aşağıdaki hello bakarak kullandığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="51507-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="51507-156"><a name="passport"></a>Web uygulamaları / Node.js passport azure ad modülünü kullanarak kaynakları koruma API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="51507-157">Uygulamanızı hello Node.js passport ad modülünü kullanıyorsanız, zaten hello gerekli mantığı toohandle anahtar geçişi otomatik olarak içeriyor.</span><span class="sxs-lookup"><span data-stu-id="51507-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="51507-158">Onaylayabilirsiniz uygulama passport-Uygulamanızın app.js parçacığında aşağıdaki hello arayarak ad</span><span class="sxs-lookup"><span data-stu-id="51507-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="51507-159"><a name="vs2015"></a>Web uygulamaları / API'leri kaynakları koruma ve Visual Studio 2015 veya Visual Studio 2017 oluşturulmuş</span><span class="sxs-lookup"><span data-stu-id="51507-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="51507-160">Uygulamanızı Visual Studio 2015 ya da Visual Studio 2017 bir web uygulaması şablonu kullanılarak oluşturulan ve seçtiyseniz **iş ve Okul hesapları** hello gelen **kimlik doğrulamayı Değiştir** menüsünde, zaten Merhaba gerekli mantığı toohandle anahtar geçişi otomatik olarak sahiptir.</span><span class="sxs-lookup"><span data-stu-id="51507-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="51507-161">OWIN Openıd Connect Hello Ara yazılımında katıştırılmış bu mantığı alır ve hello anahtarlarını hello Openıd Connect bulma belgesinden önbelleğe alır ve bunları düzenli aralıklarla yeniler.</span><span class="sxs-lookup"><span data-stu-id="51507-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="51507-162">Kimlik doğrulama tooyour çözüm elle eklediyseniz, uygulamanızın hello gerekli anahtar geçişi mantığı sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="51507-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="51507-163">Toowrite gerekir, kendinize veya izleyin hello adımları [Web uygulamaları / diğer kitaplıkları'nı kullanarak veya el ile Merhaba hiçbirini uygulama API'leri Desteklenen protokoller.](#other).</span><span class="sxs-lookup"><span data-stu-id="51507-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="51507-164"><a name="vs2013"></a>Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="51507-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="51507-165">Uygulamanızı Visual Studio 2013'te bir web uygulaması şablonu kullanılarak oluşturulan ve seçtiyseniz **Kurumsal hesaplar** hello gelen **kimlik doğrulamayı Değiştir** menüsünde hello gerekli zaten var mantığı toohandle rollover otomatik olarak anahtar.</span><span class="sxs-lookup"><span data-stu-id="51507-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="51507-166">Bu mantık, kuruluşunuzun benzersiz tanımlayıcı ve iki veritabanı tablolardaki hello projeyle ilişkili anahtar bilgileri imzalama hello depolar.</span><span class="sxs-lookup"><span data-stu-id="51507-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="51507-167">Merhaba bağlantı dizesi hello veritabanı için hello projenin Web.config dosyasında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51507-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="51507-168">Kimlik doğrulama tooyour çözüm elle eklediyseniz, uygulamanızın hello gerekli anahtar geçişi mantığı sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="51507-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="51507-169">Toowrite gerekir, kendinize veya izleyin hello adımları [Web uygulamaları / diğer kitaplıkları'nı kullanarak veya el ile Merhaba hiçbirini uygulama API'leri Desteklenen protokoller.](#other).</span><span class="sxs-lookup"><span data-stu-id="51507-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="51507-170">Aşağıdaki adımları hello hello mantığı uygulamanızda düzgün çalıştığını doğrulamak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="51507-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="51507-171">Visual Studio 2013'te hello çözümü açın ve üzerinde hello ardından **Sunucu Gezgini** hello sağ penceresi sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="51507-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="51507-172">Genişletme **veri bağlantıları**, **DefaultConnection**ve ardından **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="51507-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="51507-173">Merhaba bulun **IssuingAuthorityKeys** tablo, sağ tıklatın ve ardından **Show Table Data**.</span><span class="sxs-lookup"><span data-stu-id="51507-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="51507-174">Merhaba, **IssuingAuthorityKeys** tablo, hello anahtar toohello parmak izi değeri karşılık gelen en az bir satır olacak.</span><span class="sxs-lookup"><span data-stu-id="51507-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="51507-175">Merhaba tablodaki herhangi bir satır silin.</span><span class="sxs-lookup"><span data-stu-id="51507-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="51507-176">Sağ hello **kiracılar** tablo ve ardından **Show Table Data**.</span><span class="sxs-lookup"><span data-stu-id="51507-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="51507-177">Merhaba, **kiracılar** tablo, tooa benzersiz dizin Kiracı tanımlayıcısı karşılık gelen en az bir satır olacak.</span><span class="sxs-lookup"><span data-stu-id="51507-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="51507-178">Merhaba tablodaki herhangi bir satır silin.</span><span class="sxs-lookup"><span data-stu-id="51507-178">Delete any rows in hello table.</span></span> <span data-ttu-id="51507-179">Her iki hello hello satırlarda silmezseniz **kiracılar** tablo ve **IssuingAuthorityKeys** tablo, çalışma zamanında bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="51507-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="51507-180">Derleme ve hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="51507-180">Build and run hello application.</span></span> <span data-ttu-id="51507-181">Tooyour hesabında oturum açtıktan sonra Merhaba uygulaması durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51507-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="51507-182">Toohello iade **Sunucu Gezgini** ve hello başlangıç değerleri bakmak **IssuingAuthorityKeys** ve **kiracılar** tablo.</span><span class="sxs-lookup"><span data-stu-id="51507-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="51507-183">Bunlar otomatik olarak uygun bilgilerle hello Federasyon meta veri belgesi hello yeniden olduğunu fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="51507-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="51507-184"><a name="vs2013"></a>Kaynakları koruma ve Visual Studio 2013 ile oluşturulan web API'leri</span><span class="sxs-lookup"><span data-stu-id="51507-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="51507-185">Bir web API uygulamasını hello Web API şablonu kullanarak Visual Studio 2013'oluşturduysanız ve ardından seçili **Kurumsal hesaplar** hello gelen **kimlik doğrulamayı Değiştir** menüsünde, zaten sahip hello Uygulamanızı gerekli mantığı.</span><span class="sxs-lookup"><span data-stu-id="51507-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="51507-186">Kimlik doğrulama el ile yapılandırdıysanız, hello toolearn aşağıda nasıl yönergeleri tooconfigure Web API tooautomatically anahtar bilgilerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="51507-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="51507-187">Merhaba aşağıdaki kod parçacığını nasıl tooget hello Federasyon meta veri belgesi son anahtarları hello ve hello kullan gösterir [JWT belirteci işleyicisi](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello belirteci.</span><span class="sxs-lookup"><span data-stu-id="51507-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="51507-188">Hello kod parçacığını bir veritabanı, yapılandırma dosyası veya başka bir yerde olması gerekmediğini kendi gelecekteki kalıcı hello anahtar toovalidate mekanizma önbelleğe alma belirteçleri Azure AD'den kullanılacağını varsayar.</span><span class="sxs-lookup"><span data-stu-id="51507-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="51507-189"><a name="vs2012"></a>Kaynakları koruma ve Visual Studio 2012 ile oluşturulan web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="51507-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="51507-190">Uygulamanızı Visual Studio 2012'de oluşturulduysa, büyük olasılıkla hello kimlik ve erişim aracı tooconfigure uygulamanızı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51507-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="51507-191">Ayrıca hello kullanıyorsanız büyük olasılıkla [doğrulama verenin adı kayıt defteri (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="51507-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="51507-192">Güvenilen kimlik sağlayıcıları (Azure AD) hakkında bilgi Hello VINR sorumludur ve onlar tarafından yayınlanan toovalidate belirteçleri hello anahtarları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51507-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="51507-193">Merhaba VINR ayrıca kolay tooautomatically güncelleştirme hello anahtar bilgileri hello yapılandırması son hello ile güncel ise denetimi, bir dizinle ilişkili hello son Federasyon meta veri belgesi yükleyerek bir Web.config dosyasında depolanan kılar Belge ve güncelleştirme hello uygulama toouse hello yeni anahtarı gerekli.</span><span class="sxs-lookup"><span data-stu-id="51507-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="51507-194">Uygulamanızı hello kod örnekleri ya da Microsoft tarafından sağlanan izlenecek belgelerine herhangi birini kullanarak oluşturduysanız, hello anahtar geçişi mantığı zaten projenizde dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="51507-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="51507-195">Aşağıdaki hello kodu zaten projenizde var. fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="51507-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="51507-196">Uygulamanız bu mantığı yoksa ve düzgün çalıştığını tooverify tooadd hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="51507-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="51507-197">İçinde **Çözüm Gezgini**, başvuru toohello ekleme **System.IdentityModel** hello uygun proje için derleme.</span><span class="sxs-lookup"><span data-stu-id="51507-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="51507-198">Açık hello **Global.asax.cs** dosya ve hello aşağıdaki yönergeleri kullanarak:</span><span class="sxs-lookup"><span data-stu-id="51507-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="51507-199">Yöntem toohello aşağıdaki hello eklemek **Global.asax.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="51507-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="51507-200">Merhaba çağırma **RefreshValidationSettings()** hello yönteminde **Application_Start()** yönteminde **Global.asax.cs** gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="51507-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="51507-201">Bu adımları uyguladıktan sonra uygulamanızın Web.config hello hello Federasyon meta veri belgesi hello son anahtarları dahil olmak üzere, en son bilgilerle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="51507-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="51507-202">Bu güncelleştirme, IIS, uygulama havuzu geri dönüştürme sayısı her zaman meydana gelir; Varsayılan olarak IIS, 29 saatte toorecycle uygulamaları ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="51507-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="51507-203">Merhaba anahtar geçişi mantığı çalışma tooverify Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="51507-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="51507-204">Uygulamanızı yukarıdaki, açık hello hello kodu kullandığını doğruladıktan sonra **Web.config** dosya ve toohello gidin  **<issuerNameRegistry>**  bloğu, özellikle birkaç satır aşağıdaki Merhaba aranıyor:</span><span class="sxs-lookup"><span data-stu-id="51507-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="51507-205">Merhaba,  **<add thumbprint=””>**  ayarı ile farklı bir karakterle değiştirerek hello parmak izi değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="51507-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="51507-206">Merhaba Kaydet **Web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="51507-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="51507-207">Merhaba uygulaması oluşturmak ve ardından çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="51507-207">Build hello application, and then run it.</span></span> <span data-ttu-id="51507-208">Merhaba oturum açma işlemini tamamlamak, uygulamanız başarıyla hello anahtarı, dizinin Federasyon meta verileri belgeden gerekli hello bilgilerini indirerek güncelleştiriyor.</span><span class="sxs-lookup"><span data-stu-id="51507-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="51507-209">Oturum açma sorunları yaşıyorsanız, uygulamanızda hello değişiklikleri doğru hello okuyarak olduğundan emin olun [ekleme oturum açma tooYour Web uygulaması kullanarak Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) konusuna veya indiriliyor ve aşağıdaki kod örneği hello inceleniyor: [ Azure Active Directory için çok Kiracılı bulut uygulaması](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="51507-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="51507-210"><a name="vs2010"></a>Kaynakları koruma ve Visual Studio 2008 veya 2010 ile oluşturulan web uygulamaları ve Windows Identity Foundation (WIF) v1.0 .NET 3.5 için</span><span class="sxs-lookup"><span data-stu-id="51507-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="51507-211">Bir uygulama WIF v1.0 oluşturulduysa, uygulamanızın yapılandırma toouse yeni bir anahtar yok sağlanan mekanizması tooautomatically yenileme yoktur.</span><span class="sxs-lookup"><span data-stu-id="51507-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="51507-212">*En kolay yolu* hello WIF hello son meta veri belgesi alabilir ve yapılandırmanızı güncelleştirmek SDK dahil hello FedUtil araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="51507-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="51507-213">Merhaba System ad alanında bulunan WIF hello en yeni sürümünü içeren, uygulama too.NET 4.5, güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="51507-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="51507-214">Merhaba sonra kullanabileceğiniz [doğrulama verenin adı kayıt defteri (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform otomatik olarak güncelleştirilmesini hello uygulamanın yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="51507-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="51507-215">Bu kılavuzu belge hello sonunda hello yönergeleri göredir el ile geçiş gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="51507-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="51507-216">Toouse hello FedUtil tooupdate yapılandırmanızı yönergeler:</span><span class="sxs-lookup"><span data-stu-id="51507-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="51507-217">Merhaba WIF v1.0 SDK geliştirme makinenizde Visual Studio 2008 veya 2010 yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="51507-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="51507-218">Yapabilecekleriniz [buradan indirin](https://www.microsoft.com/en-us/download/details.aspx?id=4451) henüz yüklemediyseniz.</span><span class="sxs-lookup"><span data-stu-id="51507-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="51507-219">Merhaba çözümü Visual Studio'da açın ve ardından hello geçerli projesine sağ tıklatın ve **güncelleştirme Federasyon meta verileri**.</span><span class="sxs-lookup"><span data-stu-id="51507-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="51507-220">Bu seçenek kullanılabilir durumda değilse, FedUtil ve/veya hello WIF v1.0 SDK yüklenmedi.</span><span class="sxs-lookup"><span data-stu-id="51507-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="51507-221">Merhaba isteminden seçin **güncelleştirme** Federasyon meta verilerini güncelleştirme toobegin.</span><span class="sxs-lookup"><span data-stu-id="51507-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="51507-222">Merhaba uygulaması barındırıldığı erişim toohello sunucu ortamınız varsa, isteğe bağlı olarak FedUtil'ın kullanabilirsiniz [otomatik meta veri güncelleştirme zamanlayıcı](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="51507-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="51507-223">Tıklatın **son** toocomplete hello güncelleştirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="51507-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="51507-224"><a name="other"></a>Web uygulamaları / kaynakları koruma API'leri kullanarak diğer kitaplıkları veya el ile Merhaba hiçbirini uygulama protokolleri desteklenmez</span><span class="sxs-lookup"><span data-stu-id="51507-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="51507-225">Desteklenen hello protokollerden herhangi birini el ile uygulanan veya başka bir kitaplık kullanıyorsanız, tooreview hello kitaplığı gerekir veya anahtar Merhaba, uygulama tooensure hello Openıd Connect bulma belge veya hello alınıyor Federasyon meta veri belgesi.</span><span class="sxs-lookup"><span data-stu-id="51507-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="51507-226">Bunun için tek yönlü toocheck toodo kodunuzu veya hello kitaplığın kod arama tüm çağrıları tooeither hello Openıd bulma belge veya hello Federasyon meta veri belgesi için ' dir.</span><span class="sxs-lookup"><span data-stu-id="51507-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="51507-227">Anahtarı depolanıyor yere veya sabit kodlanmış uygulamanızda el ile Merhaba anahtar ve buna göre tarafından gerçekleştirmek hello yönergeleri Bu kılavuzu belge hello sonunda göredir el ile bir rollover güncelleştirme alın.</span><span class="sxs-lookup"><span data-stu-id="51507-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="51507-228">**Kesinlikle uygulama toosupport otomatik geçişi artırmak teşvik edilir** hello birini kullanarak yaklaşıyor anahat Bu makale tooavoid gelecekteki kesintilerini ve ek yükü içinde Azure AD, rollover tempoyla artırır veya varsa bir Acil Durum bant dışı geçişi.</span><span class="sxs-lookup"><span data-stu-id="51507-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="51507-229">Nasıl tootest etkilenecek olan ise, uygulama toodetermine</span><span class="sxs-lookup"><span data-stu-id="51507-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="51507-230">Merhaba komut dosyaları indirip hello yönergelerini takip otomatik anahtar geçişi, uygulamanızın destekleyip desteklemediğini doğrulamak için [bu GitHub depo.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="51507-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="51507-231">Nasıl tooperform uygulama, otomatik geçişi desteklemiyorsa, el ile geçiş</span><span class="sxs-lookup"><span data-stu-id="51507-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="51507-232">Uygulamanız varsa **değil** otomatik geçişi destekler, buna göre düzenli aralıklarla izleyiciler Azure AD imzalama işlemi anahtarları ve el ile geçiş işlemini gerçekleştirir tooestablish gerekir.</span><span class="sxs-lookup"><span data-stu-id="51507-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="51507-233">[Bu GitHub deposunu](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) komut dosyası ve yönergeler içeren toodo bu.</span><span class="sxs-lookup"><span data-stu-id="51507-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

