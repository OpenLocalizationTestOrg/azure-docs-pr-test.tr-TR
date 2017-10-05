---
title: "Node.js kullanarak bir Azure Active Directory v2.0 web API güvenliğini | Microsoft Docs"
description: "Node.js web kişisel bir Microsoft hesabı ve iş belirteçleri kabul eder API'si oluşturma ya da Okul hesapları öğrenin."
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
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="afbaa-103">Node.js kullanarak bir web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="afbaa-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="afbaa-104">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="afbaa-105">V2.0 uç noktası veya v1.0 uç nokta kullanması gerekip gerekmediğini belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="afbaa-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="afbaa-106">Azure Active Directory (Azure AD) v2.0 uç noktası kullandığınızda, kullanabileceğiniz [OAuth 2.0](active-directory-v2-protocols.md) erişim belirteçleri web API korumak için.</span><span class="sxs-lookup"><span data-stu-id="afbaa-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="afbaa-107">OAuth 2.0 erişim belirteçleri, hem bir kişisel Microsoft hesabı ve iş sahip kullanıcılar veya Okul hesapları web API güvenli bir şekilde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="afbaa-108">*Passport*, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="afbaa-109">Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan hiçbir Express tabanlı veya restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="afbaa-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="afbaa-110">Passport, bir dizi kapsamlı strateji kimlik doğrulamasını bir kullanıcı adı ve parola, Facebook, Twitter veya diğer seçenekleri kullanarak destekler.</span><span class="sxs-lookup"><span data-stu-id="afbaa-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="afbaa-111">Azure AD için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="afbaa-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="afbaa-112">Bu makalede, modülünü yüklemek ve Azure AD eklemek nasıl gösteriyoruz `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="afbaa-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="afbaa-113">İndir</span><span class="sxs-lookup"><span data-stu-id="afbaa-113">Download</span></span>
<span data-ttu-id="afbaa-114">Bu öğretici için kod [GitHub'da](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs) korunur.</span><span class="sxs-lookup"><span data-stu-id="afbaa-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="afbaa-115">Öğreticiyi izlemek için şunları yapabilirsiniz [uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="afbaa-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="afbaa-116">Bu öğretici sonunda tamamlanmış uygulama da alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="afbaa-117">1: bir uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="afbaa-117">1: Register an app</span></span>
<span data-ttu-id="afbaa-118">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya izleyin [bu adımları ayrıntılı](active-directory-v2-app-registration.md) uygulama kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="afbaa-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="afbaa-119">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="afbaa-119">Make sure you:</span></span>

* <span data-ttu-id="afbaa-120">Kopya **uygulama kimliği** uygulamanıza atanmış.</span><span class="sxs-lookup"><span data-stu-id="afbaa-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="afbaa-121">Bu öğretici için gerekir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="afbaa-122">Ekleme **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="afbaa-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="afbaa-123">Kopya **yeniden yönlendirme URI'si** portalından.</span><span class="sxs-lookup"><span data-stu-id="afbaa-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="afbaa-124">Varsayılan URI değeri kullanmalısınız `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="afbaa-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="afbaa-125">2: Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="afbaa-125">2: Install Node.js</span></span>
<span data-ttu-id="afbaa-126">Bu öğretici için örnek kullanmak için şunları yapmalısınız [Node.js yüklemek](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="afbaa-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="afbaa-127">3: MongoDB yükleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-127">3: Install MongoDB</span></span>
<span data-ttu-id="afbaa-128">Bu örneği başarılı bir şekilde kullanmak için [MongoDB yükleme](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="afbaa-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="afbaa-129">Bu örnekte, REST API'nizi sunucu örneklerinde kalıcı yapma MongoDB kullanın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="afbaa-130">Bu makalede, MongoDB için varsayılan yükleme ve sunucu uç noktalarını kullanmak istediğinizi varsayarız: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="afbaa-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="afbaa-131">4: restify modüllerini web API'nize yükleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="afbaa-132">Bizim REST API oluşturmak için Resitfy kullanırız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="afbaa-133">Restify, Express'ten türetilen minimal ve esnek Node.js uygulama çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="afbaa-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="afbaa-134">Restify Connect üstünde REST API'leri oluşturmak için kullanabileceğiniz özellikler sağlam bir kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="afbaa-135">Restify'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-135">Install restify</span></span>
1.  <span data-ttu-id="afbaa-136">Bir komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="afbaa-137">Varsa **azuread'i** directory olmayabilir, oluşturun:</span><span class="sxs-lookup"><span data-stu-id="afbaa-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="afbaa-138">Restify'ı yükleme:</span><span class="sxs-lookup"><span data-stu-id="afbaa-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="afbaa-139">Bu komutun çıktısı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="afbaa-139">The output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="afbaa-140">Hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="afbaa-140">Did you get an error?</span></span>
<span data-ttu-id="afbaa-141">Bazı işletim sistemlerinde kullandığınızda, `npm` komutu, bu iletiyi görebilirsiniz: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="afbaa-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="afbaa-142">Hata hesabı yönetici olarak çalıştırmayı deneyin bir istek tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="afbaa-143">Bu gerçekleşirse, komutunu `sudo` çalıştırmak için `npm` daha yüksek bir ayrıcalık düzeyinde.</span><span class="sxs-lookup"><span data-stu-id="afbaa-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="afbaa-144">DTrace için ilgili bir hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="afbaa-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="afbaa-145">Yüklediğinizde restify, bu iletiyi görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="afbaa-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="afbaa-146">Restify DTrace kullanarak REST çağrılarını izleme için güçlü bir mekanizma vardır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="afbaa-147">Ancak, DTrace birçok işletim sistemlerinde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="afbaa-148">Bu iletiyi güvenle yok sayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="afbaa-149">5: yükleme Passport.js, Web API</span><span class="sxs-lookup"><span data-stu-id="afbaa-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="afbaa-150">Komut isteminde dizini değiştirin **azuread'i**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="afbaa-151">Passport.js yükleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="afbaa-152">Komut çıktısı şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="afbaa-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="afbaa-153">6: passport azure ad web API ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="afbaa-154">Ardından, passport-azuread'i kullanarak OAuth stratejisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="afbaa-155">`passport-azuread`Azure AD'yi Passport'a bağlayan stratejileri paketidir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="afbaa-156">Bu REST API'si örneğindeki taşıyıcı belirteçler için bu stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="afbaa-157">OAuth 2.0 herhangi bir bilinen belirteç türünün verilebilmesi için bir çerçeve sağlasa da, belirli belirteç türleri yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="afbaa-158">Taşıyıcı belirteçlerini uç noktaları korumak için yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="afbaa-159">Taşıyıcı belirteçlerini OAuth 2.0 belirteç en yaygın olarak verilen türüdür.</span><span class="sxs-lookup"><span data-stu-id="afbaa-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="afbaa-160">Birçok OAuth 2.0 uygulamaları taşıyıcı belirteçlerini tek belirteç türü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="afbaa-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="afbaa-161">Bir komut isteminde dizini değiştirin **azuread'i**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="afbaa-162">Passport.js yükleme `passport-azure-ad` Modülü:</span><span class="sxs-lookup"><span data-stu-id="afbaa-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="afbaa-163">Komut çıktısı şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="afbaa-163">The output of the command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="afbaa-164">7: web API MongoDB modülleri ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="afbaa-165">Bu örnekte, bizim veri deposu olarak MongoDB kullanırız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="afbaa-166">Mongoose, yaygın olarak kullanılan bir yükleme eklentisi, model ve şemaları yönetmek için:</span><span class="sxs-lookup"><span data-stu-id="afbaa-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="afbaa-167">MongoDB olarak da adlandırılan MongoDB veritabanı sürücüsünü yükleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="afbaa-168">8: ek modülleri yükleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-168">8: Install additional modules</span></span>
<span data-ttu-id="afbaa-169">Kalan gerekli modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="afbaa-170">Bir komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="afbaa-171">Aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-171">Enter the following commands.</span></span> <span data-ttu-id="afbaa-172">Komutları node_modules dizininizde aşağıdaki modüllerini yükleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-172">The commands install the following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="afbaa-173">9: bağımlılıklarınızı için bir Server.js dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="afbaa-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="afbaa-174">Bir Server.js dosyası web API sunucunuz için işlevselliğin çoğu tutar.</span><span class="sxs-lookup"><span data-stu-id="afbaa-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="afbaa-175">Kodunuzu çoğu bu dosyaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-175">Add most of your code to this file.</span></span> <span data-ttu-id="afbaa-176">Üretim amaçları doğrultusunda, daha küçük dosyalar halinde işlevselliği gibi ayrı yollar ve denetleyiciler için yeniden.</span><span class="sxs-lookup"><span data-stu-id="afbaa-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="afbaa-177">Bu makalede, bu amaçla Server.js kullanırız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="afbaa-178">Bir komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="afbaa-179">Bir düzenleyiciyi kullanarak, bir Server.js dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="afbaa-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="afbaa-180">Aşağıdaki bilgileri dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-180">Add the following information to the file:</span></span>

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

3.  <span data-ttu-id="afbaa-181">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-181">Save the file.</span></span> <span data-ttu-id="afbaa-182">İçin kısa bir süre içinde döndürür.</span><span class="sxs-lookup"><span data-stu-id="afbaa-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="afbaa-183">10: Azure AD ayarlarınızı depolamak için bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="afbaa-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="afbaa-184">Bu kod dosyası Passport.js için Azure AD Portalı'ndan yapılandırma parametrelerini geçirir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="afbaa-185">Makaleyi başındaki portal web API'si eklendiğinde bu yapılandırma değerlerini oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="afbaa-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="afbaa-186">Kodu kopyaladıktan sonra bu parametre değerleri put gerekenler açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="afbaa-187">Bir komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="afbaa-188">Bir düzenleyicide bir Config.js dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="afbaa-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="afbaa-189">Aşağıdaki bilgileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="afbaa-190">Gerekli değerler</span><span class="sxs-lookup"><span data-stu-id="afbaa-190">Required values</span></span>

*   <span data-ttu-id="afbaa-191">**IdentityMetadata**: Bu yerdir `passport-azure-ad` kimlik sağlayıcıyı (IDP) ve anahtarları JSON Web belirteçleri (Jwt'ler) doğrulamak için yapılandırma verilerinizi arar.</span><span class="sxs-lookup"><span data-stu-id="afbaa-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="afbaa-192">Azure AD kullanıyorsanız muhtemelen bunu değiştirmek istemiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="afbaa-193">**Hedef kitle**: portalından, yeniden yönlendirme URI'si.</span><span class="sxs-lookup"><span data-stu-id="afbaa-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="afbaa-194">Anahtarlarınızı sık aralıklarla alma.</span><span class="sxs-lookup"><span data-stu-id="afbaa-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="afbaa-195">Her zaman "openid_keys" URL'den çekme ve uygulama Internet erişebildiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="afbaa-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="afbaa-196">11: Server.js dosyanıza yapılandırma ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="afbaa-197">Yeni oluşturduğunuz yapılandırma dosyasından değerleri okumaya uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="afbaa-198">Gerekli bir kaynak olarak uygulamanıza .config dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="afbaa-199">Config.js içinde olanlar için genel değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="afbaa-200">Komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="afbaa-201">Bir düzenleyicide Server.js açın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-201">In an editor, open Server.js.</span></span> <span data-ttu-id="afbaa-202">Aşağıdaki bilgileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="afbaa-203">Yeni bir bölüm için Server.js ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="afbaa-204">12: Mongoose kullanarak MongoDB model ve şema bilgilerini ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="afbaa-205">Ardından, bu üç dosyayı REST API hizmetinde bağlayın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="afbaa-206">Bu makalede, bizim görevleri depolamak üzere Mongodb'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="afbaa-207">Bu konuda aşağıdakiler ele *4. adım*.</span><span class="sxs-lookup"><span data-stu-id="afbaa-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="afbaa-208">11. adımda oluşturduğunuz Config.js dosyasında veritabanınızın adlı *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="afbaa-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="afbaa-209">Ne mongoose_auth_local bağlantı URL'si sonuna eklediğiniz öğeydi.</span><span class="sxs-lookup"><span data-stu-id="afbaa-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="afbaa-210">Bu veritabanını MongoDB'de önceden oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="afbaa-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="afbaa-211">Veritabanı (veritabanı zaten mevcut olduğu varsayılarak) sunucu uygulamasının ilk çalıştırılmasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="afbaa-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="afbaa-212">Sunucuya hangi MongoDB veritabanını kullanacak şekilde söylediyse.</span><span class="sxs-lookup"><span data-stu-id="afbaa-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="afbaa-213">Ardından, model ve şema sunucunuzun görevler için oluşturmak için bazı ek kod yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="afbaa-214">Modeli</span><span class="sxs-lookup"><span data-stu-id="afbaa-214">The model</span></span>
<span data-ttu-id="afbaa-215">Şema modeli oldukça basittir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-215">The schema model is very basic.</span></span> <span data-ttu-id="afbaa-216">Gerekirse genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="afbaa-217">Şema modeli bu değerlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="afbaa-217">The schema model has these values:</span></span>

*   <span data-ttu-id="afbaa-218">**AD**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-218">**NAME**.</span></span> <span data-ttu-id="afbaa-219">Göreve atanan kişi.</span><span class="sxs-lookup"><span data-stu-id="afbaa-219">The person assigned to the task.</span></span> <span data-ttu-id="afbaa-220">Bu bir **dize** değeri.</span><span class="sxs-lookup"><span data-stu-id="afbaa-220">This is a **string** value.</span></span>
*   <span data-ttu-id="afbaa-221">**GÖREV**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-221">**TASK**.</span></span> <span data-ttu-id="afbaa-222">Görev adı.</span><span class="sxs-lookup"><span data-stu-id="afbaa-222">The name of the task.</span></span> <span data-ttu-id="afbaa-223">Bu bir **dize** değeri.</span><span class="sxs-lookup"><span data-stu-id="afbaa-223">This is a **string** value.</span></span>
*   <span data-ttu-id="afbaa-224">**TARİH**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-224">**DATE**.</span></span> <span data-ttu-id="afbaa-225">Görev son tarihi.</span><span class="sxs-lookup"><span data-stu-id="afbaa-225">The date that the task is due.</span></span> <span data-ttu-id="afbaa-226">Bu bir **datetime** değeri.</span><span class="sxs-lookup"><span data-stu-id="afbaa-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="afbaa-227">**TAMAMLANAN**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-227">**COMPLETED**.</span></span> <span data-ttu-id="afbaa-228">Görev olup olmadığını tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="afbaa-228">Whether the task is completed.</span></span> <span data-ttu-id="afbaa-229">Bu bir **Boolean** değeri.</span><span class="sxs-lookup"><span data-stu-id="afbaa-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="afbaa-230">Kod içinde şema oluşturma</span><span class="sxs-lookup"><span data-stu-id="afbaa-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="afbaa-231">Bir komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="afbaa-232">Server.js, düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-232">In your editor, open Server.js.</span></span> <span data-ttu-id="afbaa-233">Aşağıdaki bilgileri yapılandırma girdisi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="afbaa-234">Bu kod MongoDB sunucusuna bağlanır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="afbaa-235">Ayrıca, bir şema nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="afbaa-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="afbaa-236">Şeması'nı kullanarak, modelinizi kod oluşturma</span><span class="sxs-lookup"><span data-stu-id="afbaa-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="afbaa-237">Önceki kodun altına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="afbaa-238">İlk koddan anlayabilirsiniz gibi şemanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="afbaa-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="afbaa-239">Ardından, bir model nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="afbaa-239">Next, you create a model object.</span></span> <span data-ttu-id="afbaa-240">Model nesnesi tanımlarken kod genelindeki verilerinizi depolamak için kullandığınız, **yollar**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="afbaa-241">13: görev REST API sunucunuz için yollar</span><span class="sxs-lookup"><span data-stu-id="afbaa-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="afbaa-242">Çalışmak için bir veritabanı modeliniz olduğuna göre REST API sunucunuz için kullanacağınız yolları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="afbaa-243">Yollar hakkında restify</span><span class="sxs-lookup"><span data-stu-id="afbaa-243">About routes in restify</span></span>
<span data-ttu-id="afbaa-244">Yollar restify iş tam olarak Express yığınını kullandıklarında yaparlar aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="afbaa-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="afbaa-245">Yolları, istemci uygulamalarının çağırmasını beklediğiniz URI'yi kullanarak tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="afbaa-246">Genellikle, yollarınızı ayrı bir dosyaya tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="afbaa-247">Bu öğreticide, biz Server.js bizim yollar yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="afbaa-248">Üretim kullanımı için kendi dosyasına yollar faktörü öneririz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="afbaa-249">Bir restify yolu için genel bir desen aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="afbaa-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="afbaa-250">En temel düzeyde düzeni budur.</span><span class="sxs-lookup"><span data-stu-id="afbaa-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="afbaa-251">Restify (ve hızlı) uygulama türleri ve farklı uç noktalar arasında karmaşık yönlendirme tanımlama yeteneği gibi çok daha kapsamlı işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="afbaa-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="afbaa-252">Sunucunuza varsayılan yollar ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-252">Add default routes to your server</span></span>
<span data-ttu-id="afbaa-253">Temel CRUD yollarını ekleyin: **oluşturma**, **almak**, **güncelleştirme**, ve **silmek**.</span><span class="sxs-lookup"><span data-stu-id="afbaa-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="afbaa-254">Bir komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="afbaa-255">Bir düzenleyicide Server.js açın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-255">In an editor, open Server.js.</span></span> <span data-ttu-id="afbaa-256">Aşağıda, daha önce gerçekleştirdiğiniz veritabanı girişlerinin, aşağıdaki bilgileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
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
    req.log.warn(err, 'createTask: unable to save');
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
    'removeTask: unable to delete %s',
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
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
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
    log.warn(err, "There are no tasks in the database. Add one!");
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

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="afbaa-257">Yollar için hata işleme ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-257">Add error handling for the routes</span></span>
<span data-ttu-id="afbaa-258">İstemciye, karşılaşılan sorunla ilgili iletişim kurabilmesi bazı hata işleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="afbaa-259">Zaten yazdığınız kodun altına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="afbaa-260">14: sunucunuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="afbaa-260">14: Create your server</span></span>
<span data-ttu-id="afbaa-261">Server örneğinizi eklemek için son bir şey yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="afbaa-262">Sunucu örneği çağrılarınızı yönetir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-262">The server instance manages your calls.</span></span>

<span data-ttu-id="afbaa-263">Restify (ve hızlı) bir REST API sunucusu ile kullanabileceğiniz kapsamlı özelleştirme sahip.</span><span class="sxs-lookup"><span data-stu-id="afbaa-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="afbaa-264">Bu öğreticide, en temel kurulumu kullanırız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-264">In this tutorial, we use the most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst to 10.
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
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="afbaa-265">15: (kimlik doğrulaması olmadan, şimdilik) yollar ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="afbaa-266">16: sunucunun çalıştırın</span><span class="sxs-lookup"><span data-stu-id="afbaa-266">16: Run the server</span></span>
<span data-ttu-id="afbaa-267">Kimlik doğrulaması eklemeden önce sunucunuzu test etmek için iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="afbaa-268">Sunucunuzu test etmek için en kolay yolu, bir komut isteminde curl kullanarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="afbaa-269">Bunu yapmak için çıktıyı JSON olarak ayrıştırmanıza için kullanabileceğiniz basit bir yardımcı program gerekir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="afbaa-270">Aşağıdaki örneklerde kullanırız JSON aracını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="afbaa-271">Bu işlem, JSON aracını global olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="afbaa-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="afbaa-272">MongoDB örneğinizin çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="afbaa-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="afbaa-273">Dizinine değiştirin **azuread'i**, ve ardından curl çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="afbaa-273">Change the directory to **azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="afbaa-274">Bir görev eklemek için:</span><span class="sxs-lookup"><span data-stu-id="afbaa-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="afbaa-275">Yanıt şu şekilde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="afbaa-275">The response should be:</span></span>

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

5.  <span data-ttu-id="afbaa-276">Liste görevler Brandon için:</span><span class="sxs-lookup"><span data-stu-id="afbaa-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="afbaa-277">Bu komutlar hatasız çalıştırırsanız, OAuth REST API sunucusuna eklemek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="afbaa-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="afbaa-278">*Şimdi MongoDB bir REST API sunucusuna sahipsiniz!*</span><span class="sxs-lookup"><span data-stu-id="afbaa-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="afbaa-279">17: REST API sunucunuza kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="afbaa-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="afbaa-280">Çalışan bir REST API sahip olduğunuza göre bunu Azure AD ile kullanmak şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="afbaa-281">Bir komut isteminde dizini değiştirin **azuread'i**:</span><span class="sxs-lookup"><span data-stu-id="afbaa-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="afbaa-282">Passport-azure-ad ile eklemiştir oıdcbearerstrategy'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="afbaa-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="afbaa-283">Şu ana kadar herhangi türde bir yetkilendirme olmadan genel bir REST TODO sunucusu temel aldık.</span><span class="sxs-lookup"><span data-stu-id="afbaa-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="afbaa-284">Şimdi, kimlik doğrulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-284">Now, add authentication.</span></span>

<span data-ttu-id="afbaa-285">İlk olarak, Passport'u kullanmak istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="afbaa-286">Bu hak, önceki sunucu yapılandırması sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="afbaa-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="afbaa-287">API'leri yazarken her zaman veri benzersiz kullanıcının yanılmayacağı belirteçten bağlamak için iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="afbaa-288">Bu sunucu, Yapılacaklar öğelerini depoladığında, bunları kullanıcı abonelik kimliği (token.sub olarak adlandırılır) belirteci göre depolar.</span><span class="sxs-lookup"><span data-stu-id="afbaa-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="afbaa-289">"Sahip" alanına token.sub yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="afbaa-290">Bu, yalnızca o kullanıcıyı kullanıcının TODOs erişebilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="afbaa-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="afbaa-291">Girilen TODOs başka hiç kimse erişemez.</span><span class="sxs-lookup"><span data-stu-id="afbaa-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="afbaa-292">"Sahip" API'sinde hiçbir Etkilenme yok</span><span class="sxs-lookup"><span data-stu-id="afbaa-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="afbaa-293">Bir dış kullanıcı kimlikleri doğrulanır olsa bile diğer kullanıcıların TODOs isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="afbaa-294">Ardından, birlikte Aç kimliği bağlanmak taşıyıcı stratejisi kullanın `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="afbaa-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="afbaa-295">Bu, ne önceki yapıştırdığınız sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="afbaa-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
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
log.info('verifying the user');
log.info(token, 'was the token retrieved');
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

<span data-ttu-id="afbaa-296">Passport, tüm kendi stratejileri (Twitter, Facebook vb.) benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="afbaa-297">Tüm strateji yazıcıları desene bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="afbaa-298">Stratejisi geçirmek bir `function()` bir belirteç kullanan ve `done` parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="afbaa-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="afbaa-299">Tüm iş yaptıktan sonra strateji döndürülür.</span><span class="sxs-lookup"><span data-stu-id="afbaa-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="afbaa-300">Kullanıcıyı depolayın ve böylece bunları yeniden istemeniz gerekmez belirteci kaydedin;.</span><span class="sxs-lookup"><span data-stu-id="afbaa-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afbaa-301">Önceki kod sunucunuza doğrulanabilir herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="afbaa-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="afbaa-302">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-302">This is known as auto-registration.</span></span> <span data-ttu-id="afbaa-303">Bir üretim sunucusunda herkes bunları seçtiğiniz bir kayıt sürecinden geçerler gerekmeden let istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="afbaa-304">Bu genellikle tüketici uygulamalarında görürsünüz düzeni olur.</span><span class="sxs-lookup"><span data-stu-id="afbaa-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="afbaa-305">Uygulama, Facebook ile kaydetmenize olanak sağlayabilir, ancak ek bilgileri girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="afbaa-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="afbaa-306">Bu öğretici için bir komut satırı programı doğru kullanıyorsanız, döndürülen belirteç nesnesinden e-posta ayıklanamıyor.</span><span class="sxs-lookup"><span data-stu-id="afbaa-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="afbaa-307">Sonra ek bilgilerini girmesini isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="afbaa-308">Bu bir test sunucusu olduğundan, bellek içi veritabanına doğrudan kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="afbaa-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="afbaa-309">Uç noktaları koruma</span><span class="sxs-lookup"><span data-stu-id="afbaa-309">Protect endpoints</span></span>
<span data-ttu-id="afbaa-310">Uç noktaları belirterek koruma **passport.authenticate()** kullanmak istediğiniz protokolü ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="afbaa-311">Daha gelişmiş bir seçenek için sunucu kodunuzdaki, rota düzenleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="afbaa-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="afbaa-312">18: sunucu uygulamanızı yeniden çalıştırma</span><span class="sxs-lookup"><span data-stu-id="afbaa-312">18: Run your server application again</span></span>
<span data-ttu-id="afbaa-313">Curl noktalarınızı karşı OAuth 2.0 koruma olup olmadığını görmek için yeniden kullanın.</span><span class="sxs-lookup"><span data-stu-id="afbaa-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="afbaa-314">Bu uç noktaya karşı herhangi bir istemci SDK'ları çalıştırmadan önce bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="afbaa-315">Döndürülen üst bilgiler, kimlik doğrulama düzgün çalışıp çalışmadığını söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="afbaa-316">MongoDB isntance çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="afbaa-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="afbaa-317">Dönüştür **azuread'i** dizin ve kullanım curl:</span><span class="sxs-lookup"><span data-stu-id="afbaa-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="afbaa-318">Temel bir POST deneyin:</span><span class="sxs-lookup"><span data-stu-id="afbaa-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="afbaa-319">Bir 401 yanıtına Passport katmanının tam olarak ne olduğu uç noktayı yetkilendirmek için yeniden yönlendirme yaptığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="afbaa-320">*OAuth 2.0 kullanan bir REST API hizmet artık elinizde!*</span><span class="sxs-lookup"><span data-stu-id="afbaa-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="afbaa-321">Bir OAuth 2.0 ile uyumlu istemci kullanmadan bu sunucu ile kadar gitti.</span><span class="sxs-lookup"><span data-stu-id="afbaa-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="afbaa-322">Bunun için ek bir öğretici gözden gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="afbaa-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afbaa-323">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="afbaa-323">Next steps</span></span>
<span data-ttu-id="afbaa-324">Başvuru için tamamlanan örnek (yapılandırma değerleriniz olmadan) olarak sağlanan [bir .zip dosyası](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="afbaa-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="afbaa-325">Aynı zamanda Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="afbaa-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="afbaa-326">Şimdi, daha ileri seviyeli konulara geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="afbaa-327">Denemek isteyebilirsiniz [v2.0 uç noktası ile bir Node.js web uygulaması güvenli](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="afbaa-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="afbaa-328">Bazı ek kaynaklar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="afbaa-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="afbaa-329">Azure AD v2.0 Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="afbaa-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="afbaa-330">Yığın taşması "azure-active-directory" etiketi</span><span class="sxs-lookup"><span data-stu-id="afbaa-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="afbaa-331">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="afbaa-331">Get security updates for our products</span></span>
<span data-ttu-id="afbaa-332">Güvenlik olayları oluştuğunda bildirim almak için kaydolun öneririz.</span><span class="sxs-lookup"><span data-stu-id="afbaa-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="afbaa-333">Üzerinde [Microsoft Teknik Güvenlik bildirimleri](https://technet.microsoft.com/security/dd252948) sayfasında, güvenlik danışma uyarılara abone.</span><span class="sxs-lookup"><span data-stu-id="afbaa-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

