---
title: "Azure AD Node.js Başlarken | Microsoft Docs"
description: "Node.js REST web kimlik doğrulaması için Azure AD ile tümleştirilir API'si oluşturma."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="ad03d-103">Node.js için Web API ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ad03d-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ad03d-104">*Passport*, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="ad03d-105">Esnek ve modüler, Passport sorunsuz bir şekilde her Express tabanlı bırakılabilir veya Restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="ad03d-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="ad03d-106">Bir dizi kapsamlı strateji bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ad03d-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="ad03d-107">Microsoft Azure Active Directory için (Azure AD) bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="ad03d-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ad03d-108">Bu modülü yükleyin ve ardından Microsoft Azure Active Directory ekleyin `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="ad03d-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="ad03d-109">Bunu yapmanız için gerekenler:</span><span class="sxs-lookup"><span data-stu-id="ad03d-109">To do this, you need to:</span></span>

1. <span data-ttu-id="ad03d-110">Bir uygulamayı Azure AD'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="ad03d-111">Passport'un kullanmak için uygulamanızı ayarlayın `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="ad03d-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="ad03d-112">Yapılacaklar listesi web API'sini çağırmak için bir istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="ad03d-113">Bu öğretici için kod [GitHub'da](https://github.com/Azure-Samples/active-directory-node-webapi) korunur.</span><span class="sxs-lookup"><span data-stu-id="ad03d-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="ad03d-114">Bu makalede, oturum açma, kaydolma nasıl uygulanacağını veya Azure AD B2C ile profil Yönetimi kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="ad03d-115">Kullanıcının kimliği zaten doğrulanmış sonra web API'leri çağırmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="ad03d-116">İle başlamanızı öneririz [Azure Active Directory belge ile tümleştirmek nasıl](active-directory-how-to-integrate.md) Azure Active Directory ile ilgili temel bilgileri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="ad03d-117">Biz GitHub çalışan bu örnekte bir MIT lisansı altında için tüm kaynak kodunu yayımlanan, bu nedenle kopya (veya çatalı bile daha iyi) çekinmeyin ve geri bildirim sağlamak ve çekme istekleri.</span><span class="sxs-lookup"><span data-stu-id="ad03d-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="ad03d-118">Node.js modüllerini hakkında</span><span class="sxs-lookup"><span data-stu-id="ad03d-118">About Node.js modules</span></span>
<span data-ttu-id="ad03d-119">Bu kılavuzda Node.js modüllerini kullanırız.</span><span class="sxs-lookup"><span data-stu-id="ad03d-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="ad03d-120">Modüller, uygulamanız için belirli işlevler sağlayan yüklenebilir JavaScript paketlerdir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="ad03d-121">Genellikle NPM yükleme dizininde Node.js NPM komut satırı aracını kullanarak modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="ad03d-122">Ancak, HTTP modülü gibi bazı modüller çekirdek Node.js pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="ad03d-123">Yüklü modülleri kaydedilir **node_modules** Node.js yükleme dizinine kökündeki dizin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="ad03d-124">Her bir modülü **node_modules** directory tutar kendi **node_modules** bağımlı herhangi bir modül içeren dizini.</span><span class="sxs-lookup"><span data-stu-id="ad03d-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="ad03d-125">Ayrıca, her gerekli modülüne sahip bir **node_modules** dizini.</span><span class="sxs-lookup"><span data-stu-id="ad03d-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="ad03d-126">Bu özyinelemeli dizin yapısını bağımlılık zinciri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ad03d-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="ad03d-127">Bu bağımlılık zinciri yapı daha büyük bir uygulama yer sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="ad03d-128">Ancak, ayrıca tüm bağımlılıkları karşılanırsa ve geliştirme kullanılan modülleri sürümünü üretimde kullanılır güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="ad03d-129">Bu, üretim uygulamanızın davranışını daha tahmin edilebilir hale getirir ve kullanıcıları etkileyebilecek sürüm oluşturma sorunları önler.</span><span class="sxs-lookup"><span data-stu-id="ad03d-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="ad03d-130">1. adım: Azure AD kiracısı kaydetme</span><span class="sxs-lookup"><span data-stu-id="ad03d-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="ad03d-131">Bu örneği kullanmak için Azure Active Directory kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="ad03d-132">Hangi Kiracı ya da bir alma, emin değilseniz bkz [Azure AD kiracısı alma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ad03d-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="ad03d-133">2. adım: uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad03d-133">Step 2: Create an application</span></span>
<span data-ttu-id="ad03d-134">Sonraki dizininizde, uygulamanız ile güvenli bir şekilde iletişim kurması için gereken bilgileri Azure AD'ye verir bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad03d-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="ad03d-135">Hem istemci uygulaması hem de web API'si tek bir tarafından temsil edilen **uygulama kimliği** bu durumda, bir mantıksal uygulama içerdikleri için.</span><span class="sxs-lookup"><span data-stu-id="ad03d-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="ad03d-136">Bir uygulama oluşturmak için [bu talimatları](active-directory-how-applications-are-added.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="ad03d-137">Bir satır iş kolu uygulaması geliştiriyorsanız [bu ek yönergeler yararlı olabilecek](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ad03d-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="ad03d-138">Bir uygulama oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="ad03d-138">To create an application:</span></span>

1. <span data-ttu-id="ad03d-139">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ad03d-140">Üst menüsünde hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-140">On the top menu, select your account.</span></span> <span data-ttu-id="ad03d-141">Ardından, altında **Directory** listesinde, Active Directory Kiracı uygulamanızı kaydetmek istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="ad03d-142">Soldaki menüde seçin **daha Hizmetleri**ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="ad03d-143">Seçin **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="ad03d-144">Oluşturmak için istemleri izleyerek bir **Web uygulaması ve/veya Webapı**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="ad03d-145">**Adı** uygulamanızı son kullanıcıların uygulamayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="ad03d-146">**Oturum açma URL'si** , uygulamanızın temel URL.</span><span class="sxs-lookup"><span data-stu-id="ad03d-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="ad03d-147">Örnek kod, varsayılan URL `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="ad03d-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="ad03d-148">Kaydettikten sonra Azure AD, uygulamanızın benzersiz bir uygulama kimliği atar</span><span class="sxs-lookup"><span data-stu-id="ad03d-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="ad03d-149">Bu değer gereken sonraki bölümlerde, bu nedenle uygulama sayfasından kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="ad03d-150">Gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="ad03d-151">**Uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="ad03d-152">Kuralı kullanmaktır `https://<tenant-domain>/<app-name>`, örneğin: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="ad03d-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="ad03d-153">Oluşturma bir **anahtar** uygulamanızdan için **ayarları** sayfasında ve bir yere kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="ad03d-154">Kısa süre içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="ad03d-155">3. adım: Platformunuz için Node.js indirme</span><span class="sxs-lookup"><span data-stu-id="ad03d-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="ad03d-156">Bu örneği başarılı bir şekilde kullanmak için Node.js çalışan yüklemesine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="ad03d-157">Adresinden node.js'yi yükleyin [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ad03d-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="ad03d-158">4. adım: Yükleme MongoDB, platformda</span><span class="sxs-lookup"><span data-stu-id="ad03d-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="ad03d-159">Bu örneği başarılı bir şekilde kullanmak için MongoDB çalışan yüklemesine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="ad03d-160">Mongodb'yi, REST API sunucu örneklerinde kalıcı yapmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="ad03d-161">Adresinden [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="ad03d-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="ad03d-162">Bu kılavuz, mongodb://localhost bu yazma zamanında olduğu, MongoDB için varsayılan yükleme ve sunucu uç noktalarını kullanmak varsayar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="ad03d-163">5. adım: Restify modüllerini web API'nize yükleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="ad03d-164">Bizim REST API oluşturmak için Restify kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="ad03d-165">Restify, Express'ten türetilen minimal ve esnek Node.js uygulama çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="ad03d-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="ad03d-166">Connect üstünde REST API'leri oluşturmaya yönelik bir dizi sağlam özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="ad03d-167">Restify'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-167">Install Restify</span></span>
1. <span data-ttu-id="ad03d-168">Komut satırında, dizinleri değiştirmek **azuread'i** dizini.</span><span class="sxs-lookup"><span data-stu-id="ad03d-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="ad03d-169">Varsa **azuread'i** directory olmayabilir, oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad03d-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="ad03d-170">Aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="ad03d-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="ad03d-171">Bu komut Restify'ı yükler.</span><span class="sxs-lookup"><span data-stu-id="ad03d-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="ad03d-172">Hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="ad03d-172">Did you get an error?</span></span>
<span data-ttu-id="ad03d-173">Bazı işletim sistemlerinde NPM kullandığınızda bildiren bir hata alabilirsiniz **hata: EPERM, chmod ' / usr/yerel/bin /..'**</span><span class="sxs-lookup"><span data-stu-id="ad03d-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="ad03d-174">ve öneride hesabı yönetici olarak çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="ad03d-175">Bu gerçekleşirse, NPM daha yüksek bir ayrıcalık düzeyinde çalıştırmak için sudo komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="ad03d-176">DTRACE ilgili bir hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="ad03d-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="ad03d-177">Restify'ı yüklerken şuna benzer bir hata görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ad03d-177">You might see an error like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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
<span data-ttu-id="ad03d-178">Restify, DTrace kullanarak REST çağrılarını izlemek için güçlü bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="ad03d-179">Bununla birlikte, birçok işletim sistemi DTrace gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ad03d-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="ad03d-180">Bu hataları güvenle yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="ad03d-181">Bu komutun çıktısı aşağıdaki çıkış benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ad03d-181">The output of this command should look similar to the following output:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="ad03d-182">6. adım: Yükleme Passport.js, Web API</span><span class="sxs-lookup"><span data-stu-id="ad03d-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="ad03d-183">[Passport](http://passportjs.org/), Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="ad03d-184">Esnek ve modüler, Passport sorunsuz bir şekilde her Express tabanlı bırakılabilir veya Restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="ad03d-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="ad03d-185">Bir dizi kapsamlı strateji bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ad03d-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="ad03d-186">Azure Active Directory için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="ad03d-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="ad03d-187">Biz bu modülü yükleyin ve ardından Azure Active Directory stratejisi eklentisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="ad03d-188">Komut satırında, dizinleri değiştirmek **azuread'i** dizini.</span><span class="sxs-lookup"><span data-stu-id="ad03d-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="ad03d-189">Passport.js yüklemek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="ad03d-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="ad03d-190">Komut çıktısı şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ad03d-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="ad03d-191">7. adım: Passport Azure AD web API'nize ekleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="ad03d-192">Sonraki OAuth stratejisini kullanarak eklediğimiz `passport-azure-ad`, Passport Azure Active Directory connect stratejileri dizisi.</span><span class="sxs-lookup"><span data-stu-id="ad03d-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="ad03d-193">Bu REST API'si örneğindeki taşıyıcı belirteçler için bu stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="ad03d-194">OAuth2 herhangi bir bilinen belirteç türünün verilebilir bir altyapı sağlasa da yalnızca belirli belirteç türleri yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="ad03d-195">Taşıyıcı belirteçleri uç noktaları korumak için en yaygın kullanılan belirteçleridir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="ad03d-196">Bunlar OAuth2 belirteci en yaygın olarak verilen türüdür.</span><span class="sxs-lookup"><span data-stu-id="ad03d-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="ad03d-197">Birçok uygulama, taşıyıcı belirteçlerini düzenlenen belirteçlerin türü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="ad03d-198">Komut satırında, dizinleri değiştirmek **azuread'i** dizini.</span><span class="sxs-lookup"><span data-stu-id="ad03d-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="ad03d-199">Passport.js yüklemek için aşağıdaki komutu yazın `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="ad03d-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="ad03d-200">Komutunun çıktısını aşağıdaki çıkış benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ad03d-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="ad03d-201">8. adım: Web API'nize MongoDB modülleri ekleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="ad03d-202">Bizim veri deposu olarak MongoDB kullanırız.</span><span class="sxs-lookup"><span data-stu-id="ad03d-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="ad03d-203">Bu nedenle, biz model ve şemaları yönetmek için yaygın olarak kullanılan eklenti çağrılan Mongoose yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="ad03d-204">Biz de (hangi MongoDB olarak da adlandırılır) MongoDB veritabanı sürücüsünü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="ad03d-205">9. adım: ek modülleri yükleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="ad03d-206">Sonraki kalan gerekli modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="ad03d-207">Komut satırında, dizinleri değiştirmek **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="ad03d-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad03d-208">Bu modüllerdeki yüklemek için aşağıdaki komutları girin, **node_modules** dizini:</span><span class="sxs-lookup"><span data-stu-id="ad03d-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="ad03d-209">10. adım: bağımlılıklarınız ile bir server.js oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad03d-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="ad03d-210">Server.js dosyasında bizim web API sunucunuz için işlevselliğin çoğu sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="ad03d-211">Size büyük bir kısmını bu dosyaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-211">We add most of our code to this file.</span></span> <span data-ttu-id="ad03d-212">Üretim için işlevselliği, ayrı yollar ve denetleyiciler gibi daha küçük dosyalar halinde yeniden düzenlemeniz öneririz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="ad03d-213">Bu gösteride, biz bu işlevsellik için server.js kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="ad03d-214">Komut satırında, dizinleri değiştirmek **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="ad03d-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad03d-215">Oluşturma bir `server.js` dosya, en sık kullandığınız düzenleyicide ve aşağıdaki bilgileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ad03d-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="ad03d-216">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-216">Save the file.</span></span> <span data-ttu-id="ad03d-217">İçin bir kısa süre içinde getireceğiz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="ad03d-218">11. adım: Azure AD ayarlarınızı depolamak için bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad03d-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="ad03d-219">Bu kod dosyası Passport.js için Azure Active Directory portalınızdan yapılandırma parametrelerini geçirir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="ad03d-220">Portal kılavuzun ilk bölümünde web API'si eklendiğinde bu yapılandırma değerlerini oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ad03d-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="ad03d-221">Kodu kopyaladıktan sonra bu parametre değerlerine eklemeniz gerekenler açıklanacaktır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="ad03d-222">Komut satırında, dizinleri değiştirmek **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="ad03d-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad03d-223">Oluşturma bir `config.js` dosya, en sık kullandığınız düzenleyicide ve aşağıdaki bilgileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ad03d-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="ad03d-224">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="ad03d-225">12. adım: yapılandırma değerlerini server.js dosyanıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="ad03d-226">Bu değerleri uygulamamız oluşturulan .config dosyası okuma gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="ad03d-227">Bunu yapmak için .config dosyası gerekli bir kaynak olarak bizim uygulamada ekleriz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="ad03d-228">Sonra genel değişkenler config.js belge değişkenlerde eşleşecek şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="ad03d-229">Komut satırında, dizinleri değiştirmek **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="ad03d-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad03d-230">Açık, `server.js` dosya, en sık kullandığınız düzenleyicide ve aşağıdaki bilgileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ad03d-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="ad03d-231">Yeni bir bölüm eklemek `server.js` aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="ad03d-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="ad03d-232">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="ad03d-233">13. adım: Mongoose kullanarak MongoDB Model ve şema bilgilerini ekleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="ad03d-234">Şimdi Biz bu üç dosyayı REST API hizmetinde birleştirmek gibi ödeme başlatmak için bu hazırlık geçiyor.</span><span class="sxs-lookup"><span data-stu-id="ad03d-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="ad03d-235">Bu kılavuz için 4. adımda açıklandığı gibi bizim görevleri depolamak için MongoDB kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="ad03d-236">İçinde `config.js` dosya adım 11 oluşturduğumuz, biz Veritabanımıza adlı `tasklist`, biz sonunda put olduğu için bizim **mogoose_auth_local** bağlantı URL'si.</span><span class="sxs-lookup"><span data-stu-id="ad03d-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="ad03d-237">Bu veritabanını MongoDB'de önceden oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ad03d-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="ad03d-238">Bunun yerine, MongoDB bu bize (veritabanı önceden var olmayan varsayılarak) bizim sunucu uygulamasının ilk çalıştırılmasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad03d-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="ad03d-239">Biz sunucu kullanmak için isteriz hangi MongoDB veritabanını söylediyse, model ve şema bizim sunucunun görevler için oluşturmak için bazı ek kod yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="ad03d-240">Modelin tartışma</span><span class="sxs-lookup"><span data-stu-id="ad03d-240">Discussion of the model</span></span>
<span data-ttu-id="ad03d-241">Bizim şema modeli basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-241">Our schema model is simple.</span></span> <span data-ttu-id="ad03d-242">Size gereken şekilde genişletin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-242">You expand it as required.</span></span>

<span data-ttu-id="ad03d-243">Ad: Göreve atanan kişi adı.</span><span class="sxs-lookup"><span data-stu-id="ad03d-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="ad03d-244">A **dize**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-244">A **String**.</span></span>

<span data-ttu-id="ad03d-245">Görev: Görevin kendisi.</span><span class="sxs-lookup"><span data-stu-id="ad03d-245">TASK: The task itself.</span></span> <span data-ttu-id="ad03d-246">A **dize**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-246">A **String**.</span></span>

<span data-ttu-id="ad03d-247">Tarihi: görev son tarihi.</span><span class="sxs-lookup"><span data-stu-id="ad03d-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="ad03d-248">A **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-248">A **DATETIME**.</span></span>

<span data-ttu-id="ad03d-249">TAMAMLANDI: görev varsa veya tamamlanmış.</span><span class="sxs-lookup"><span data-stu-id="ad03d-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="ad03d-250">A **BOOLEAN**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="ad03d-251">Kod içinde şema oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad03d-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="ad03d-252">Komut satırında, dizinleri değiştirmek **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="ad03d-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad03d-253">Açık, `server.js` dosya, en sık kullandığınız düzenleyicide ve sonra aşağıdaki bilgileri yapılandırma girdisi altına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ad03d-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="ad03d-254">Koddan anlayabilirsiniz gibi bizim şema ilk oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="ad03d-255">Biz tanımlarken kod genelindeki verileri depolamak için kullandığımız bir model nesnesi oluşturuyoruz sonra bizim **yollar**.</span><span class="sxs-lookup"><span data-stu-id="ad03d-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="ad03d-256">14. adım: bizim görev REST API sunucunuz için bizim yollar ekleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="ad03d-257">Biz çalışmak için bir veritabanı modeliniz olduğuna göre biz giden yollar bizim REST API sunucunuz için kullanmak ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="ad03d-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="ad03d-258">Restify'daki yollar hakkında</span><span class="sxs-lookup"><span data-stu-id="ad03d-258">About routes in Restify</span></span>
<span data-ttu-id="ad03d-259">Yollar Restify'da Express yığınını yaparlar aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="ad03d-260">Yolları, istemci uygulamalarının çağırmasını beklediğiniz URI'yi kullanarak tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="ad03d-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="ad03d-261">Genellikle, yollarınızı ayrı bir dosyaya tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="ad03d-262">Bizim amacıyla, biz server.js dosyasında bizim yollar yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="ad03d-263">Üretim kullanımı için kendi dosyasına bu yollar faktörü öneririz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="ad03d-264">Bir Restify yolu için genel bir desen aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ad03d-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="ad03d-265">Bu, en temel düzeyindeki desendir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="ad03d-266">Restify (ve hızlı) uygulama türlerini tanımlama ve farklı uç noktalar arasında karmaşık yönlendirme sağlama gibi çok daha kapsamlı işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="ad03d-267">Bizim amacıyla, biz Bu yolları basit tutuyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="ad03d-268">Bizim sunucuya varsayılan yollar ekleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-268">Add default routes to our server</span></span>
<span data-ttu-id="ad03d-269">Biz şimdi temel CRUD yollarını oluşturma, alma, güncelleştirme, ekleme ve silme.</span><span class="sxs-lookup"><span data-stu-id="ad03d-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="ad03d-270">Komut satırında, dizinleri değiştirmek **azuread'i** , zaten orada değilseniz klasörü:</span><span class="sxs-lookup"><span data-stu-id="ad03d-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="ad03d-271">Açık `server.js` dosya, en sık kullandığınız düzenleyicide ve sonra aşağıdaki bilgileri yaptığınız önceki veritabanı girişlerinin altına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ad03d-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="ad03d-272">Hata işleme bizim API'leri ekleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="ad03d-273">15. adım: sunucunuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad03d-273">Step 15: Create your server</span></span>
<span data-ttu-id="ad03d-274">Veritabanımıza tanımlamış olduğunuz ve bizim yollar yerdir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="ad03d-275">Son bir şey yapmak için bizim çağrıları yöneten sunucu örneğini eklemektir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="ad03d-276">Restify'ı (ve hızlı) çok sayıda REST API sunucunuz için özelleştirme yapabilirsiniz, ancak yeniden biz en temel kurulumu bizim amaçlar için kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="ad03d-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="ad03d-277">16. adım: yolları (olmadan kimlik doğrulaması için şimdi) sunucusu ekleyin</span><span class="sxs-lookup"><span data-stu-id="ad03d-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="ad03d-278">17. adım: (OAuth desteğini eklemeden önce) sunucu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ad03d-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="ad03d-279">Biz kimlik doğrulaması eklemeden önce sunucunuzu sınayın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="ad03d-280">Sunucunuzu test etmek için en kolay yolu, komut satırında curl kullanarak ' dir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="ad03d-281">Bunu önce çıktıyı JSON olarak ayrıştırmanıza kurmamızı sağlayan bir yardımcı programı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="ad03d-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="ad03d-282">(Aşağıdaki örneklerde, bu aracı kullanın) aşağıdaki JSON aracını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ad03d-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="ad03d-283">Bu işlem, JSON aracını global olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="ad03d-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="ad03d-284">Şimdi biz elde, sunucuyla Yürüt:</span><span class="sxs-lookup"><span data-stu-id="ad03d-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="ad03d-285">Öncelikle, mongoDB örneğinizin çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="ad03d-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="ad03d-286">Ardından, dizini değiştirin ve curling başlatın:</span><span class="sxs-lookup"><span data-stu-id="ad03d-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="ad03d-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="ad03d-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="ad03d-288">Ardından, biz bu şekilde bir görev ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ad03d-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="ad03d-289">Yanıt şu şekilde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ad03d-289">The response should be:</span></span>

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
    <span data-ttu-id="ad03d-290">Ve şu görevleri bu şekilde Brandon için listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ad03d-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="ad03d-291">Tüm bu çalışırsa, biz OAuth REST API sunucusuna ekleme yapmaya hazırsınız demektir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="ad03d-292">Bir REST API MongoDB sunucusuyla var!</span><span class="sxs-lookup"><span data-stu-id="ad03d-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="ad03d-293">Adım 18: kimlik doğrulaması bizim REST API sunucusuna ekleme</span><span class="sxs-lookup"><span data-stu-id="ad03d-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="ad03d-294">Çalışan bir REST API sahibiz, Azure AD ile yararlı hale getirme başlayalım.</span><span class="sxs-lookup"><span data-stu-id="ad03d-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="ad03d-295">Komut satırında, dizinleri değiştirmek **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="ad03d-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="ad03d-296">passport-azure-ad ile birlikte dahil edilen OIDCBearerStrategy'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="ad03d-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="ad03d-297">Şu ana kadar herhangi türde bir yetkilendirme olmadan genel bir REST TODO sunucusu oluşturduğumuz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="ad03d-298">Burada, bir araya getirilmesi Başlat budur.</span><span class="sxs-lookup"><span data-stu-id="ad03d-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="ad03d-299">İlk olarak, biz biz Passport'u kullanmak istediğinizi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="ad03d-300">Bu hak, diğer sunucu yapılandırmanızın sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="ad03d-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="ad03d-301">API'leri yazarken, her zaman veri benzersiz kullanıcının yanılmayacağı belirteçten bağlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="ad03d-302">Bu sunucu, Yapılacaklar öğelerini depoladığında, bunları nesne kimliği (token.oid olarak adlandırılır), belirteçte biz "sahip" alanına yerleştirin kullanıcının göre depolar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="ad03d-303">Bu, yalnızca bu kullanıcının kendi TODOs erişebilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad03d-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="ad03d-304">Olmadığından hiçbir Etkilenme "sahip" API'SİNDE bir dış kullanıcı kimlikleri doğrulanır olsa bile başkalarının TODOs isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="ad03d-305">Sonraki birlikte taşıyıcı stratejisi kullanalım `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="ad03d-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="ad03d-306">Şimdilik koda bakın ve rest kısa süre içinde açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="ad03d-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="ad03d-307">Bu, ne yukarıda yapıştırdığınız sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="ad03d-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="ad03d-308">Passport, strateji yazarlarının hepsinin bağlı tüm kendi stratejileri (Twitter, Facebook vb.) için benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="ad03d-309">Stratejisi baktığınızda, biz bir belirteç ve yapılan bir parametre olarak olan bir işlev geçirmek bakın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="ad03d-310">Kendi iş yaptıktan sonra strateji bize gelir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="ad03d-311">Bunu yaptıktan sonra biz kullanıcıyı depolayın ve biz bunları yeniden istemeniz gerekmez belirteci kaydedin;.</span><span class="sxs-lookup"><span data-stu-id="ad03d-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad03d-312">Önceki kod olur bizim sunucusuna kimlik doğrulaması için herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="ad03d-313">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-313">This is known as auto-registration.</span></span> <span data-ttu-id="ad03d-314">Üretim sunucularında, herkesin bunları gerekmeden izin verme olduğunu öneririz karar kayıt işlemiyle gidin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="ad03d-315">Genellikle, Facebook ile kaydolursunuz ancak daha sonra ek bilgileri doldurmanızı isteyin izin tüketici uygulamalarında görürsünüz düzeni budur.</span><span class="sxs-lookup"><span data-stu-id="ad03d-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="ad03d-316">Bu komut satırı programı olmasaydı, size e-posta döndürülen ve ek bilgileri doldurmasını kullanıcıya sorulan belirteç nesnesi ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="ad03d-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="ad03d-317">Bu bir test sunucusu olduğundan bunları yalnızca bellek içi veritabanına ekleriz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="ad03d-318">Bazı uç noktaları koruma</span><span class="sxs-lookup"><span data-stu-id="ad03d-318">Protect some endpoints</span></span>
<span data-ttu-id="ad03d-319">Belirterek uç noktaları koruma `passport.authenticate()` kullanmak istediğiniz protokolü ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="ad03d-320">Bizim sunucu kodu daha ilginç bir şeyler, rota düzenleyelim yapma.</span><span class="sxs-lookup"><span data-stu-id="ad03d-320">To make our server code do something more interesting, let’s edit the route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="ad03d-321">19. adım: sunucu uygulamanızı yeniden çalıştırın ve sizi reddettiğini olun</span><span class="sxs-lookup"><span data-stu-id="ad03d-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="ad03d-322">Kullanalım `curl` yeniden biz artık OAuth2 koruma bizim uç noktalarına karşı olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="ad03d-323">Biz, herhangi bir istemci SDK Bu uç noktaya karşı çalıştırmadan önce bu test yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="ad03d-324">Döndürülen üstbilgileri doğru yolu yapacağız durumunda bize için yeterli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="ad03d-325">Öncelikle, mongoDB örneğinizin çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="ad03d-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="ad03d-326">Ardından, dizini değiştirin ve curling başlatın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="ad03d-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="ad03d-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="ad03d-328">Temel bir POST deneyin.</span><span class="sxs-lookup"><span data-stu-id="ad03d-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="ad03d-329">Bir 401 burada aradığınız cevaptır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="ad03d-330">Bu yanıt Passport katmanının tam olarak ne olduğu yetkili uç noktası için yeniden yönlendirme yaptığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad03d-331">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad03d-331">Next steps</span></span>
<span data-ttu-id="ad03d-332">OAuth2 uyumlu bir istemci kullanmadan bu sunucu ile kadar gitti.</span><span class="sxs-lookup"><span data-stu-id="ad03d-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="ad03d-333">Bir ek izlenecek yol gitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="ad03d-334">Restify ve OAuth2 kullanarak bir REST API'si uygulama artık öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="ad03d-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="ad03d-335">Ayrıca tutup hizmetinizi geliştirme göre bu örnekte nasıl oluşturulacağını öğrenmek için birden fazla yeterli kod vardır.</span><span class="sxs-lookup"><span data-stu-id="ad03d-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="ad03d-336">ADAL Yolculuğunuzun sonraki adımlarda ilgileniyorsanız, desteklenen bazı ADAL istemcileri ile çalışmaya devam öneririz aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ad03d-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="ad03d-337">Geliştirici makinenizi aşağıya doğru kopyalamak ve kılavuzda açıklandığı gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ad03d-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="ad03d-338">İOS için ADAL</span><span class="sxs-lookup"><span data-stu-id="ad03d-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="ad03d-339">Android için ADAL</span><span class="sxs-lookup"><span data-stu-id="ad03d-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
