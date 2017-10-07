---
title: Node.js kullanarak bir Azure Active Directory v2.0 web API aaaSecure | Microsoft Docs
description: "Nasıl toobuild bir Node.js web belirteçleri kişisel bir Microsoft hesabı ve iş veya Okul hesapları kabul eder API öğrenin."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="0cfc1-103">Node.js kullanarak bir web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="0cfc1-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="0cfc1-104">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="0cfc1-105">mı hello v2.0 uç noktası veya hello v1.0 uç noktası, kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="0cfc1-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="0cfc1-106">Hello Azure Active Directory (Azure AD) v2.0 uç noktası kullandığınızda, kullanabileceğiniz [OAuth 2.0](active-directory-v2-protocols.md) erişim belirteçleri tooprotect web API.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="0cfc1-107">OAuth 2.0 erişim belirteçleri, hem bir kişisel Microsoft hesabı ve iş sahip kullanıcılar veya Okul hesapları web API güvenli bir şekilde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="0cfc1-108">*Passport*, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="0cfc1-109">Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan hiçbir Express tabanlı veya restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="0cfc1-110">Passport, bir dizi kapsamlı strateji kimlik doğrulamasını bir kullanıcı adı ve parola, Facebook, Twitter veya diğer seçenekleri kullanarak destekler.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="0cfc1-111">Azure AD için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="0cfc1-112">Bu makalede, nasıl tooinstall hello modülü ve ardından hello Azure AD ekleyin gösteriyoruz `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="0cfc1-113">İndir</span><span class="sxs-lookup"><span data-stu-id="0cfc1-113">Download</span></span>
<span data-ttu-id="0cfc1-114">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="0cfc1-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="0cfc1-115">yapabilecekleriniz toofollow hello öğretici, [hello uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="0cfc1-116">Bu öğretici hello sonunda tamamlanmış Merhaba uygulaması da alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="0cfc1-117">1: bir uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="0cfc1-117">1: Register an app</span></span>
<span data-ttu-id="0cfc1-118">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya izleyin [bu adımları ayrıntılı](active-directory-v2-app-registration.md) tooregister bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="0cfc1-119">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-119">Make sure you:</span></span>

* <span data-ttu-id="0cfc1-120">Kopya hello **uygulama kimliği** tooyour uygulama atanmış.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="0cfc1-121">Bu öğretici için gerekir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="0cfc1-122">Merhaba eklemek **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="0cfc1-123">Kopya hello **yeniden yönlendirme URI'si** hello portalından.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="0cfc1-124">Merhaba varsayılan URI değeri kullanmalısınız `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="0cfc1-125">2: Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="0cfc1-125">2: Install Node.js</span></span>
<span data-ttu-id="0cfc1-126">Bu öğretici için toouse hello örnek, şunları yapmalısınız [Node.js yüklemek](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="0cfc1-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="0cfc1-127">3: MongoDB yükleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-127">3: Install MongoDB</span></span>
<span data-ttu-id="0cfc1-128">toosuccessfully Bu örneği kullanmak için şunları yapmalısınız [MongoDB yükleme](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="0cfc1-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="0cfc1-129">Bu örnekte, MongoDB toomake sunucu örneklerinde kalıcı, REST API kullanın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="0cfc1-130">Bu makalede, MongoDB için hello varsayılan yükleme ve sunucu uç noktalarını kullanmak istediğinizi varsayarız: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="0cfc1-131">4: yükleme hello restify web API modülleri</span><span class="sxs-lookup"><span data-stu-id="0cfc1-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="0cfc1-132">Bizim REST API Resitfy toobuild kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="0cfc1-133">Restify, Express'ten türetilen minimal ve esnek Node.js uygulama çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="0cfc1-134">Restify toobuild Connect üstünde REST API'leri kullanabileceğiniz özellikleri sağlam bir dizi vardır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="0cfc1-135">Restify'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-135">Install restify</span></span>
1.  <span data-ttu-id="0cfc1-136">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="0cfc1-137">Merhaba, **azuread'i** directory olmayabilir, oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="0cfc1-138">Restify'ı yükleme:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="0cfc1-139">Bu komutun çıktısı Hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-139">hello output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="0cfc1-140">Hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="0cfc1-140">Did you get an error?</span></span>
<span data-ttu-id="0cfc1-141">Bazı işletim sistemlerinde hello kullandığınızda, `npm` komutu, bu iletiyi görebilirsiniz: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="0cfc1-142">Merhaba hata, bir yönetici olarak çalışan hello hesap deneyin bir istek tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="0cfc1-143">Bu gerçekleşirse, hello komutunu `sudo` toorun `npm` daha yüksek bir ayrıcalık düzeyinde.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="0cfc1-144">İlgili hata mı aldınız tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="0cfc1-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="0cfc1-145">Yüklediğinizde restify, bu iletiyi görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="0cfc1-146">Restify DTrace kullanarak REST çağrılarını güçlü mekanizması tootrace sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="0cfc1-147">Ancak, DTrace birçok işletim sistemlerinde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="0cfc1-148">Bu iletiyi güvenle yok sayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="0cfc1-149">5: yükleme Passport.js, Web API</span><span class="sxs-lookup"><span data-stu-id="0cfc1-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="0cfc1-150">Merhaba komut isteminde hello dizini çok değiştirmek**azuread'i**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="0cfc1-151">Passport.js yükleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="0cfc1-152">Merhaba hello komutunun çıktısını aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="0cfc1-153">6: passport azure ad tooyour web API ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="0cfc1-154">Ardından, passport-azuread'i kullanarak hello OAuth stratejisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="0cfc1-155">`passport-azuread`Azure AD'yi Passport'a bağlayan stratejileri paketidir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="0cfc1-156">Bu REST API'si örneğindeki taşıyıcı belirteçler için bu stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="0cfc1-157">OAuth 2.0 herhangi bir bilinen belirteç türünün verilebilmesi için bir çerçeve sağlasa da, belirli belirteç türleri yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="0cfc1-158">Taşıyıcı belirteçlerini yaygın olarak kullanılan tooprotect noktalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="0cfc1-159">Taşıyıcı belirteçlerini en yaygın olarak verilen hello OAuth 2.0 belirteç türleridir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="0cfc1-160">Birçok OAuth 2.0 uygulamaları taşıyıcı belirteçlerini hello tek belirteç türü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="0cfc1-161">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="0cfc1-162">Merhaba Passport.js yükleme `passport-azure-ad` Modülü:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="0cfc1-163">Merhaba hello komutunun çıktısını aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-163">hello output of hello command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="0cfc1-164">7: MongoDB modülleri tooyour web API ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="0cfc1-165">Bu örnekte, bizim veri deposu olarak MongoDB kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="0cfc1-166">Mongoose, yaygın olarak kullanılan bir yükleme eklenti toomanage modelleri ve şemalar:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="0cfc1-167">Merhaba veritabanı sürücüsünü MongoDB olarak da adlandırılan MongoDB yükleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="0cfc1-168">8: ek modülleri yükleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-168">8: Install additional modules</span></span>
<span data-ttu-id="0cfc1-169">Merhaba kalan gerekli modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="0cfc1-170">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="0cfc1-171">Aşağıdaki komutları hello girin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-171">Enter hello following commands.</span></span> <span data-ttu-id="0cfc1-172">Merhaba komutları node_modules dizininizde modülleri aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-172">hello commands install hello following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="0cfc1-173">9: bağımlılıklarınızı için bir Server.js dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="0cfc1-174">Bir Server.js dosyası hello işlevselliği, web API sunucunuz için hello çoğunluğu tutar.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="0cfc1-175">Kodu toothis dosyanızda çoğunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-175">Add most of your code toothis file.</span></span> <span data-ttu-id="0cfc1-176">Üretim amaçları doğrultusunda, hello işlevselliği daha küçük dosyalar halinde gibi ayrı yollar ve denetleyiciler için yeniden.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="0cfc1-177">Bu makalede, bu amaçla Server.js kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="0cfc1-178">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="0cfc1-179">Bir düzenleyiciyi kullanarak, bir Server.js dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="0cfc1-180">Aşağıdaki bilgileri toohello dosyasına hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-180">Add hello following information toohello file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="0cfc1-181">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-181">Save hello file.</span></span> <span data-ttu-id="0cfc1-182">Kısa süre içinde tooit döndürür.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="0cfc1-183">10: Azure AD ayarlarınızı bir yapılandırma dosyası toostore oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="0cfc1-184">Bu kod dosyası, Azure AD portalı tooPassport.js hello yapılandırma parametrelerini geçirir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="0cfc1-185">Merhaba makalenin hello başında hello web API toohello portal eklendiğinde bu yapılandırma değerlerini oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="0cfc1-186">Merhaba kodu kopyaladıktan sonra hangi tooput hello değerleri bu parametrelerin açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="0cfc1-187">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="0cfc1-188">Bir düzenleyicide bir Config.js dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="0cfc1-189">Aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="0cfc1-190">Gerekli değerler</span><span class="sxs-lookup"><span data-stu-id="0cfc1-190">Required values</span></span>

*   <span data-ttu-id="0cfc1-191">**IdentityMetadata**: Bu yerdir `passport-azure-ad` hello kimlik sağlayıcıyı (IDP) ve hello anahtarları toovalidate JSON Web belirteçleri (Jwt'ler) hello için yapılandırma verilerinizi arar.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="0cfc1-192">Azure AD kullanıyorsanız muhtemelen toochange bu istemediğiniz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="0cfc1-193">**Hedef kitle**: hello Portal'dan, yeniden yönlendirme URI'si.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0cfc1-194">Anahtarlarınızı sık aralıklarla alma.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="0cfc1-195">Hello "openid_keys" URL'den her zaman çekme ve bu hello uygulama hello Internet erişebildiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="0cfc1-196">11: hello yapılandırma tooyour Server.js dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="0cfc1-197">Uygulamanızı tooread hello değerleri hello yapılandırma dosyasından yeni oluşturduğunuz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="0cfc1-198">Gerekli bir kaynak olarak uygulamanıza Hello .config dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="0cfc1-199">Config.js içinde olan hello genel değişkenler toothose ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="0cfc1-200">Merhaba komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="0cfc1-201">Bir düzenleyicide Server.js açın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-201">In an editor, open Server.js.</span></span> <span data-ttu-id="0cfc1-202">Aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="0cfc1-203">Yeni bir bölüm tooServer.js ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="0cfc1-204">12: Mongoose kullanarak hello MongoDB model ve şema bilgilerini ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="0cfc1-205">Ardından, bu üç dosyayı REST API hizmetinde bağlayın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="0cfc1-206">Bu makalede, bizim görevleri MongoDB toostore kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="0cfc1-207">Bu konuda aşağıdakiler ele *4. adım*.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="0cfc1-208">11. adımda oluşturduğunuz hello Config.js dosyasında veritabanınızın adlı *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="0cfc1-209">Hello mongoose_auth_local bağlantı URL'si sonuna eklediğiniz oluştu.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="0cfc1-210">Bu veritabanında önceden MongoDB toocreate gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="0cfc1-211">Merhaba veritabanı üzerinde hello ilk (Merhaba veritabanı zaten mevcut olduğu varsayılarak), sunucu uygulamasının çalışma oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="0cfc1-212">Hangi MongoDB veritabanı toouse hello sunucu söylediyse.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="0cfc1-213">Ardından toowrite bazı ek kod toocreate hello model ve şema sunucunuzun görevler için gerekir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="0cfc1-214">Merhaba modeli</span><span class="sxs-lookup"><span data-stu-id="0cfc1-214">hello model</span></span>
<span data-ttu-id="0cfc1-215">Hello şema modeli oldukça basittir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-215">hello schema model is very basic.</span></span> <span data-ttu-id="0cfc1-216">Gerekirse genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="0cfc1-217">Bu değerleri Hello şema modeli vardır:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="0cfc1-218">**AD**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-218">**NAME**.</span></span> <span data-ttu-id="0cfc1-219">Merhaba kişiye atanan toohello görev.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-219">hello person assigned toohello task.</span></span> <span data-ttu-id="0cfc1-220">Bu bir **dize** değeri.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-220">This is a **string** value.</span></span>
*   <span data-ttu-id="0cfc1-221">**GÖREV**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-221">**TASK**.</span></span> <span data-ttu-id="0cfc1-222">Merhaba görev Hello adı.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-222">hello name of hello task.</span></span> <span data-ttu-id="0cfc1-223">Bu bir **dize** değeri.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-223">This is a **string** value.</span></span>
*   <span data-ttu-id="0cfc1-224">**TARİH**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-224">**DATE**.</span></span> <span data-ttu-id="0cfc1-225">Başlangıç tarihi bu hello son bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-225">hello date that hello task is due.</span></span> <span data-ttu-id="0cfc1-226">Bu bir **datetime** değeri.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="0cfc1-227">**TAMAMLANAN**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-227">**COMPLETED**.</span></span> <span data-ttu-id="0cfc1-228">Merhaba görev olup olmadığını tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-228">Whether hello task is completed.</span></span> <span data-ttu-id="0cfc1-229">Bu bir **Boolean** değeri.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="0cfc1-230">Merhaba kodda Hello şema oluşturun</span><span class="sxs-lookup"><span data-stu-id="0cfc1-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="0cfc1-231">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="0cfc1-232">Server.js, düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-232">In your editor, open Server.js.</span></span> <span data-ttu-id="0cfc1-233">Aşağıdaki bilgilerle hello Hello yapılandırma girdisi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="0cfc1-234">Bu kod toohello MongoDB sunucusuna bağlanır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="0cfc1-235">Ayrıca, bir şema nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="0cfc1-236">Hello Şeması'nı kullanarak, modelinizi hello kod oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="0cfc1-237">Kod önceki hello koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="0cfc1-238">İlk hello koddan anlayabilirsiniz gibi şemanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="0cfc1-239">Ardından, bir model nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-239">Next, you create a model object.</span></span> <span data-ttu-id="0cfc1-240">Merhaba genelindeki verilerinizi tanımlarken kod hello model nesnesi toostore kullanın, **yollar**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="0cfc1-241">13: görev REST API sunucunuz için yollar</span><span class="sxs-lookup"><span data-stu-id="0cfc1-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="0cfc1-242">Veritabanı modeli toowork ile sahip olduğunuza göre REST API sunucunuz için kullanacağınız hello yolları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="0cfc1-243">Yollar hakkında restify</span><span class="sxs-lookup"><span data-stu-id="0cfc1-243">About routes in restify</span></span>
<span data-ttu-id="0cfc1-244">Yollar tam olarak hello kullandığınızda yaparlar aynı şekilde hello Express yığınını iş restify.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="0cfc1-245">Merhaba hello istemci uygulamaları toocall beklediğiniz URI kullanılarak yolları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="0cfc1-246">Genellikle, yollarınızı ayrı bir dosyaya tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="0cfc1-247">Bu öğreticide, biz Server.js bizim yollar yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="0cfc1-248">Üretim kullanımı için kendi dosyasına yollar faktörü öneririz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="0cfc1-249">Bir restify yolu için genel bir desen aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="0cfc1-250">Merhaba düzeni hello en temel düzeyde budur.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="0cfc1-251">Restify (ve hızlı) hello özelliği toodefine uygulama türleri ve farklı uç noktalar arasında karmaşık yönlendirme gibi çok daha kapsamlı işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="0cfc1-252">Varsayılan yollar tooyour sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-252">Add default routes tooyour server</span></span>
<span data-ttu-id="0cfc1-253">Merhaba temel CRUD yollarını ekleyin: **oluşturma**, **almak**, **güncelleştirme**, ve **silmek**.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="0cfc1-254">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="0cfc1-255">Bir düzenleyicide Server.js açın.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-255">In an editor, open Server.js.</span></span> <span data-ttu-id="0cfc1-256">Aşağıda, daha önce yaptığınız veritabanı girişlerini Merhaba, aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="0cfc1-257">Merhaba yollar için hata işleme ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-257">Add error handling for hello routes</span></span>
<span data-ttu-id="0cfc1-258">Karşılaştığınız hello sorun hakkında geri toohello istemci iletişim kurabilmesi bazı hata işleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="0cfc1-259">Zaten yazdıktan hello kod aşağıda koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="0cfc1-260">14: sunucunuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-260">14: Create your server</span></span>
<span data-ttu-id="0cfc1-261">Son bir şey toodo hello tooadd, sunucu örneğidir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="0cfc1-262">Merhaba sunucu örneği çağrılarınızı yönetir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="0cfc1-263">Restify (ve hızlı) bir REST API sunucusu ile kullanabileceğiniz kapsamlı özelleştirme sahip.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="0cfc1-264">Bu öğreticide, hello en temel kurulumu kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-264">In this tutorial, we use hello most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="0cfc1-265">15: (kimlik doğrulaması olmadan, şimdilik) hello yollar ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="0cfc1-266">16: hello sunucu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="0cfc1-266">16: Run hello server</span></span>
<span data-ttu-id="0cfc1-267">İyi bir fikir tootest olan kimlik doğrulaması eklemeden önce sunucunuzun.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="0cfc1-268">Merhaba en kolay yolu tootest, bir komut isteminde curl kullanarak, sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="0cfc1-269">toodo Bu, JSON olarak tooparse çıkış kullanabileceğiniz basit bir yardımcı program gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="0cfc1-270">Örnek hello kullanırız hello JSON aracını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="0cfc1-271">Bu hello JSON aracını Global olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="0cfc1-272">MongoDB örneğinizin çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="0cfc1-273">Merhaba dizini çok değiştirmek**azuread'i**, ve ardından curl çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-273">Change hello directory too**azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="0cfc1-274">bir görev tooadd:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="0cfc1-275">Merhaba yanıt şu şekilde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-275">hello response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="0cfc1-276">Liste görevler Brandon için:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="0cfc1-277">Bu komutlar hatasız çalıştırmak, hazır tooadd OAuth toohello REST API sunucusuna demektir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="0cfc1-278">*Şimdi MongoDB bir REST API sunucusuna sahipsiniz!*</span><span class="sxs-lookup"><span data-stu-id="0cfc1-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="0cfc1-279">17: kimlik doğrulama tooyour REST API sunucusu ekleme</span><span class="sxs-lookup"><span data-stu-id="0cfc1-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="0cfc1-280">Çalışan bir REST API sahip olduğunuza göre toouse ayarlama, Azure AD ile.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="0cfc1-281">Bir komut isteminde hello dizini çok değiştirmek**azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="0cfc1-282">Passport-azure-ad ile eklemiştir hello oıdcbearerstrategy'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="0cfc1-283">Şu ana kadar herhangi türde bir yetkilendirme olmadan genel bir REST TODO sunucusu temel aldık.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="0cfc1-284">Şimdi, kimlik doğrulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-284">Now, add authentication.</span></span>

<span data-ttu-id="0cfc1-285">İlk olarak, toouse Passport istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="0cfc1-286">Bu hak, önceki sunucu yapılandırması sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="0cfc1-287">API'leri yazarken, verileri toosomething kullanıcı hello hello belirteçten benzersiz yanılmayacağı iyi bir fikir tooalways bağlantı hello var.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="0cfc1-288">Bu sunucu, Yapılacaklar öğelerini depoladığında, bunları hello kullanıcı abonelik kimliği (token.sub olarak adlandırılır) hello belirtecindeki göre depolar.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="0cfc1-289">Merhaba token.sub hello "sahip" alanına yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="0cfc1-290">Bu, yalnızca o kullanıcıyı hello kullanıcının TODOs erişebilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="0cfc1-291">Hiç kimsenin girilen hello TODOs erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="0cfc1-292">"Sahip" Merhaba API içinde hiçbir Etkilenme yok</span><span class="sxs-lookup"><span data-stu-id="0cfc1-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="0cfc1-293">Bir dış kullanıcı kimlikleri doğrulanır olsa bile diğer kullanıcıların TODOs isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="0cfc1-294">Ardından, birlikte hello açık kimliği bağlanmak taşıyıcı stratejisi kullanın `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="0cfc1-295">Bu, ne önceki yapıştırdığınız sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="0cfc1-296">Passport, tüm kendi stratejileri (Twitter, Facebook vb.) benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="0cfc1-297">Tüm strateji yazıcıları toohello düzeni uyması.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="0cfc1-298">Merhaba stratejisi geçirmek bir `function()` bir belirteç kullanan ve `done` parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="0cfc1-299">tüm iş yaptıktan sonra hello stratejisi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="0cfc1-300">İçin yeniden tooask gerekmeyen şekilde hello kullanıcı ve hazırlama hello belirtecini depolar.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0cfc1-301">Merhaba önceki kod tooyour sunucu kimliğini doğrulayabilir herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="0cfc1-302">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-302">This is known as auto-registration.</span></span> <span data-ttu-id="0cfc1-303">Bir üretim sunucusunda toolet herkes bunları seçtiğiniz bir kayıt sürecinden geçerler gerekmeden istediğiniz olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="0cfc1-304">Bu genellikle tüketici uygulamalarında görürsünüz hello düzeni olur.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="0cfc1-305">Merhaba uygulama Facebook ile tooregister sağlayabilir, ancak tooenter ek bilgiler, ister.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="0cfc1-306">Bu öğretici için bir komut satırı programı doğru kullanıyorsanız, döndürülen hello belirteç nesnesinden hello e-posta ayıklanamıyor.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="0cfc1-307">Ardından, hello kullanıcı tooenter ek bilgileri isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="0cfc1-308">Bu bir test sunucusu olduğundan, hello kullanıcı ekleme doğrudan toohello bellek içi veritabanı.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="0cfc1-309">Uç noktaları koruma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-309">Protect endpoints</span></span>
<span data-ttu-id="0cfc1-310">Merhaba belirterek uç noktaları koruma **passport.authenticate()** toouse istediğiniz çağrısı hello protokolü ile.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="0cfc1-311">Daha gelişmiş bir seçenek için sunucu kodunuzdaki, rota düzenleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="0cfc1-312">18: sunucu uygulamanızı yeniden çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-312">18: Run your server application again</span></span>
<span data-ttu-id="0cfc1-313">Kullanım curl yeniden toosee noktalarınızı karşı OAuth 2.0 koruması varsa.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="0cfc1-314">Bu uç noktaya karşı herhangi bir istemci SDK'ları çalıştırmadan önce bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="0cfc1-315">döndürülen hello üstbilgileri, kimlik doğrulama düzgün çalışıp çalışmadığını söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="0cfc1-316">MongoDB isntance çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="0cfc1-317">Değiştirme toohello **azuread'i** dizin ve kullanım curl:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="0cfc1-318">Temel bir POST deneyin:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="0cfc1-319">Bir 401 yanıtına hello Passport katman tooredirect çalışıyor gösterir toohello kimlik doğrulama uç noktası, tam olarak ne olduğu.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="0cfc1-320">*OAuth 2.0 kullanan bir REST API hizmet artık elinizde!*</span><span class="sxs-lookup"><span data-stu-id="0cfc1-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="0cfc1-321">Bir OAuth 2.0 ile uyumlu istemci kullanmadan bu sunucu ile kadar gitti.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="0cfc1-322">Bunun için ek bir öğretici tooreview gerekir.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cfc1-323">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0cfc1-323">Next steps</span></span>
<span data-ttu-id="0cfc1-324">Başvuru için tamamlandı hello örnek (yapılandırma değerleriniz olmadan) olarak sağlanan [bir .zip dosyası](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0cfc1-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="0cfc1-325">Aynı zamanda Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="0cfc1-326">Şimdi, Gelişmiş konular toomore üzerinde taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="0cfc1-327">Tootry isteyebilirsiniz [hello v2.0 uç kullanarak bir Node.js web uygulaması güvenli](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="0cfc1-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="0cfc1-328">Bazı ek kaynaklar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0cfc1-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="0cfc1-329">Azure AD v2.0 Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="0cfc1-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="0cfc1-330">Yığın taşması "azure-active-directory" etiketi</span><span class="sxs-lookup"><span data-stu-id="0cfc1-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="0cfc1-331">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="0cfc1-331">Get security updates for our products</span></span>
<span data-ttu-id="0cfc1-332">Güvenlik olayları olduğunda bildirim toobe yukarı toosign öneririz.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="0cfc1-333">Merhaba üzerinde [Microsoft Teknik Güvenlik bildirimleri](https://technet.microsoft.com/security/dd252948) sayfasında, tooSecurity danışma uyarıları abone olun.</span><span class="sxs-lookup"><span data-stu-id="0cfc1-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

