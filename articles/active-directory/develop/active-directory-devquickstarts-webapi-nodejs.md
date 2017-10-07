---
title: "aaaAzure AD Node.js Başlarken | Microsoft Docs"
description: "Nasıl toobuild bir Node.js REST web API'si, kimlik doğrulaması için Azure AD ile tümleşir."
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
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="59e9b-103">Node.js için Web API ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="59e9b-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="59e9b-104">*Passport*, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="59e9b-105">Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan tooany Express tabanlı veya Restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="59e9b-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="59e9b-106">Bir dizi kapsamlı strateji bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="59e9b-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="59e9b-107">Microsoft Azure Active Directory için (Azure AD) bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="59e9b-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="59e9b-108">Bu modülü yükleyin ve ardından hello Microsoft Azure Active Directory ekleyin `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="59e9b-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="59e9b-109">toodo bunu yapmanız:</span><span class="sxs-lookup"><span data-stu-id="59e9b-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="59e9b-110">Bir uygulamayı Azure AD'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="59e9b-111">Uygulama toouse Passport's ayarlamak `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="59e9b-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="59e9b-112">Bir istemci uygulama toocall hello tooDo listesi web API yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="59e9b-113">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="59e9b-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="59e9b-114">Bu makalede nasıl tooimplement oturum açma kapsamıyordur, kaydolma, veya profil Yönetimi Azure AD B2C ile.</span><span class="sxs-lookup"><span data-stu-id="59e9b-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="59e9b-115">Merhaba kullanıcının kimliği zaten doğrulanmış sonra web API'leri çağırmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="59e9b-116">İle başlamanızı öneririz [nasıl toointegrate Azure Active Directory belgeyle](active-directory-how-to-integrate.md) toolearn Azure Active Directory hello temelleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="59e9b-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="59e9b-117">Tüm hello kaynak kodu github'da çalışan bu örneğin bir MIT lisansı altında yayımladık şekilde eşitleyerek ücretsiz tooclone (veya hatta daha iyi çatalı) ve geri bildirim sağlamak ve çekme istekleri.</span><span class="sxs-lookup"><span data-stu-id="59e9b-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="59e9b-118">Node.js modüllerini hakkında</span><span class="sxs-lookup"><span data-stu-id="59e9b-118">About Node.js modules</span></span>
<span data-ttu-id="59e9b-119">Bu kılavuzda Node.js modüllerini kullanırız.</span><span class="sxs-lookup"><span data-stu-id="59e9b-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="59e9b-120">Modüller, uygulamanız için belirli işlevler sağlayan yüklenebilir JavaScript paketlerdir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="59e9b-121">Modüller genellikle hello NPM yükleme dizininde hello Node.js NPM komut satırı aracını kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="59e9b-122">Ancak, hello HTTP modülü gibi bazı modüller hello çekirdek Node.js paketinde dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="59e9b-123">Yüklü modülleri hello kaydedilir **node_modules** hello kökündeki Node.js yükleme dizininin dizin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="59e9b-124">Merhaba her modülünde **node_modules** directory tutar kendi **node_modules** bağımlı herhangi bir modül içeren dizini.</span><span class="sxs-lookup"><span data-stu-id="59e9b-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="59e9b-125">Ayrıca, her gerekli modülüne sahip bir **node_modules** dizini.</span><span class="sxs-lookup"><span data-stu-id="59e9b-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="59e9b-126">Bu özyinelemeli dizin yapısını hello bağımlılık zinciri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="59e9b-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="59e9b-127">Bu bağımlılık zinciri yapı daha büyük bir uygulama yer sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="59e9b-128">Ancak, ayrıca tüm bağımlılıkları karşılanırsa ve geliştirme kullanılan hello sürümünün hello modüllerin de üretimde kullanılan güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="59e9b-129">Bu hello üretim uygulamanızın davranışını daha tahmin edilebilir hale getirir ve kullanıcıları etkileyebilecek sürüm oluşturma sorunları önler.</span><span class="sxs-lookup"><span data-stu-id="59e9b-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="59e9b-130">1. adım: Azure AD kiracısı kaydetme</span><span class="sxs-lookup"><span data-stu-id="59e9b-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="59e9b-131">toouse Bu örnek, Azure Active Directory kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="59e9b-132">Emin değilseniz, hangi bir kiracı veya nasıl tooget, bkz. [nasıl tooget bir Azure AD Kiracı](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="59e9b-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="59e9b-133">2. adım: uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="59e9b-133">Step 2: Create an application</span></span>
<span data-ttu-id="59e9b-134">Sonraki toosecurely ihtiyaç duyduğu verir Azure AD bilgilerini uygulamanız ile iletişim kurması dizininizde bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59e9b-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="59e9b-135">Merhaba istemci uygulaması ve web API tarafından tek bir temsil **uygulama kimliği** bu durumda, bir mantıksal uygulama içerdikleri için.</span><span class="sxs-lookup"><span data-stu-id="59e9b-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="59e9b-136">Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="59e9b-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="59e9b-137">Bir satır iş kolu uygulaması geliştiriyorsanız [bu ek yönergeler yararlı olabilecek](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="59e9b-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="59e9b-138">bir uygulama toocreate:</span><span class="sxs-lookup"><span data-stu-id="59e9b-138">toocreate an application:</span></span>

1. <span data-ttu-id="59e9b-139">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="59e9b-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="59e9b-140">Merhaba üst menüsünde hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-140">On hello top menu, select your account.</span></span> <span data-ttu-id="59e9b-141">Ardından, hello altında **Directory** listesinde, uygulamanızın hello Active Directory Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="59e9b-142">Merhaba soldaki Hello menüde seçin **daha Hizmetleri**ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="59e9b-143">Seçin **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="59e9b-144">Merhaba istemleri toocreate izleyin bir **Web uygulaması ve/veya Webapı**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="59e9b-145">Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın açıklar.</span><span class="sxs-lookup"><span data-stu-id="59e9b-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="59e9b-146">Merhaba **oturum açma URL'si** , uygulamanızın hello temel URL'dir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="59e9b-147">Merhaba hello örnek kod URL'sidir varsayılan `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="59e9b-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="59e9b-148">Kaydettikten sonra Azure AD, uygulamanızın benzersiz bir uygulama kimliği atar</span><span class="sxs-lookup"><span data-stu-id="59e9b-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="59e9b-149">Bu değer ihtiyacınız hello sonraki bölümlerde, bu nedenle hello uygulama sayfadan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="59e9b-150">Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="59e9b-151">Merhaba **uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="59e9b-152">Merhaba kuraldır toouse `https://<tenant-domain>/<app-name>`, örneğin: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="59e9b-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="59e9b-153">Oluşturma bir **anahtar** hello uygulamanızdan için **ayarları** sayfasında ve bir yere kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="59e9b-154">Kısa süre içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="59e9b-155">3. adım: Platformunuz için Node.js indirme</span><span class="sxs-lookup"><span data-stu-id="59e9b-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="59e9b-156">Bu örnek toosuccessfully kullanın, Node.js çalışan yüklemesine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="59e9b-157">Adresinden node.js'yi yükleyin [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="59e9b-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="59e9b-158">4. adım: Yükleme MongoDB, platformda</span><span class="sxs-lookup"><span data-stu-id="59e9b-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="59e9b-159">toosuccessfully kullanın Bu örnek, MongoDB çalışan yüklemesine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="59e9b-160">Sunucu örneklerinde kalıcı REST API MongoDB toomake hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="59e9b-161">Adresinden [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="59e9b-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="59e9b-162">Bu kılavuzda mongodb://localhost hello zaman bu yazma olduğu hello varsayılan yükleme ve sunucu uç noktalarını MongoDB için kullandığını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="59e9b-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="59e9b-163">5. adım: Merhaba Restify modüllerini web API'nize yükleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="59e9b-164">Bizim REST API Restify toobuild kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="59e9b-165">Restify, Express'ten türetilen minimal ve esnek Node.js uygulama çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="59e9b-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="59e9b-166">Connect üstünde REST API'leri oluşturmaya yönelik bir dizi sağlam özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="59e9b-167">Restify'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-167">Install Restify</span></span>
1. <span data-ttu-id="59e9b-168">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** dizini.</span><span class="sxs-lookup"><span data-stu-id="59e9b-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="59e9b-169">Merhaba, **azuread'i** directory olmayabilir, oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59e9b-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="59e9b-170">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="59e9b-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="59e9b-171">Bu komut Restify'ı yükler.</span><span class="sxs-lookup"><span data-stu-id="59e9b-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="59e9b-172">Hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="59e9b-172">Did you get an error?</span></span>
<span data-ttu-id="59e9b-173">Bazı işletim sistemlerinde NPM kullandığınızda bildiren bir hata alabilirsiniz **hata: EPERM, chmod ' / usr/yerel/bin /..'**</span><span class="sxs-lookup"><span data-stu-id="59e9b-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="59e9b-174">ve öneride çalışan hello hesabı yönetici olarak deneyin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="59e9b-175">Bu durum oluşursa, daha yüksek bir ayrıcalık düzeyinde hello sudo komutu toorun NPM kullanın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="59e9b-176">DTRACE ilgili bir hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="59e9b-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="59e9b-177">Restify'ı yüklerken şuna benzer bir hata görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="59e9b-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="59e9b-178">Restify, DTrace kullanarak REST çağrılarını izlemek için güçlü bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e9b-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="59e9b-179">Bununla birlikte, birçok işletim sistemi DTrace gerekmez.</span><span class="sxs-lookup"><span data-stu-id="59e9b-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="59e9b-180">Bu hataları güvenle yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="59e9b-181">Bu komutun çıktısı Hello benzer toohello çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="59e9b-181">hello output of this command should look similar toohello following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="59e9b-182">6. adım: Yükleme Passport.js, Web API</span><span class="sxs-lookup"><span data-stu-id="59e9b-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="59e9b-183">[Passport](http://passportjs.org/), Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="59e9b-184">Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan tooany Express tabanlı veya Restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="59e9b-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="59e9b-185">Bir dizi kapsamlı strateji bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="59e9b-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="59e9b-186">Azure Active Directory için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="59e9b-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="59e9b-187">Biz bu modülü yükleyin ve ardından hello Azure Active Directory stratejisi eklentisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="59e9b-188">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** dizini.</span><span class="sxs-lookup"><span data-stu-id="59e9b-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="59e9b-189">tooinstall passport.js hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="59e9b-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="59e9b-190">Merhaba hello komutunun çıkışını benzer toohello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="59e9b-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="59e9b-191">7. adım: Passport Azure AD tooyour web API ekleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="59e9b-192">Sonraki hello OAuth stratejisini kullanarak eklediğimiz `passport-azure-ad`, Azure Active Directory tooPassport bağlanmak stratejileri dizisi.</span><span class="sxs-lookup"><span data-stu-id="59e9b-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="59e9b-193">Bu REST API'si örneğindeki taşıyıcı belirteçler için bu stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="59e9b-194">OAuth2 herhangi bir bilinen belirteç türünün verilebilir bir altyapı sağlasa da yalnızca belirli belirteç türleri yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="59e9b-195">Taşıyıcı belirteçleri uç noktaları korumak için en yaygın olarak kullanılan hello belirteçleridir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="59e9b-196">Bunlar en yaygın olarak verilen hello OAuth2 belirteci türüdür.</span><span class="sxs-lookup"><span data-stu-id="59e9b-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="59e9b-197">Birçok uygulama, taşıyıcı belirteçlerini hello türündeki tek düzenlenen belirteçlerin olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="59e9b-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="59e9b-198">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** dizini.</span><span class="sxs-lookup"><span data-stu-id="59e9b-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="59e9b-199">Türü hello şu komutu tooinstall hello Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="59e9b-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="59e9b-200">Merhaba hello komutunun çıkışını benzer toohello çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="59e9b-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="59e9b-201">8. adım: MongoDB modülleri tooyour web API ekleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="59e9b-202">Bizim veri deposu olarak MongoDB kullanırız.</span><span class="sxs-lookup"><span data-stu-id="59e9b-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="59e9b-203">Bu nedenle, tooinstall ihtiyacımız hello yaygın olarak kullanılan eklenti çağrılan Mongoose toomanage model ve şemaları.</span><span class="sxs-lookup"><span data-stu-id="59e9b-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="59e9b-204">Ayrıca tooinstall hello veritabanı sürücüsünü (hangi MongoDB olarak da adlandırılır) MongoDB için ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="59e9b-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="59e9b-205">9. adım: ek modülleri yükleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="59e9b-206">Sonraki hello kalan gerekli modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="59e9b-207">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="59e9b-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="59e9b-208">Bu modüllerdeki komutlar tooinstall aşağıdaki hello girin, **node_modules** dizini:</span><span class="sxs-lookup"><span data-stu-id="59e9b-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="59e9b-209">10. adım: bağımlılıklarınız ile bir server.js oluşturma</span><span class="sxs-lookup"><span data-stu-id="59e9b-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="59e9b-210">Merhaba server.js dosyası hello işlevselliğinin bizim web API sunucunuz için sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e9b-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="59e9b-211">Bizim kod toothis dosyasını çoğunu ekleriz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-211">We add most of our code toothis file.</span></span> <span data-ttu-id="59e9b-212">Üretim amaçları doğrultusunda hello işlevselliği, ayrı yollar ve denetleyiciler gibi daha küçük dosyalar halinde yeniden düzenlemeniz öneririz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="59e9b-213">Bu gösteride, biz bu işlevsellik için server.js kullanın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="59e9b-214">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="59e9b-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="59e9b-215">Oluşturma bir `server.js` dosya, en sık kullandığınız düzenleyicide ve ardından aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="59e9b-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

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

3. <span data-ttu-id="59e9b-216">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-216">Save hello file.</span></span> <span data-ttu-id="59e9b-217">Kısa süre içinde tooit getireceğiz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="59e9b-218">11. adım: Azure AD ayarlarınızı bir yapılandırma dosyası toostore oluşturma</span><span class="sxs-lookup"><span data-stu-id="59e9b-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="59e9b-219">Bu kod dosyası, Azure Active Directory portal tooPassport.js hello yapılandırma parametrelerini geçirir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="59e9b-220">Merhaba kılavuzun hello ilk bölümü hello web API toohello portal eklendiğinde bu yapılandırma değerlerini oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="59e9b-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="59e9b-221">Merhaba kodu kopyaladıktan sonra biz hello değerleri bu parametre hangi tooput açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="59e9b-222">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="59e9b-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="59e9b-223">Oluşturma bir `config.js` dosya, en sık kullandığınız düzenleyicide ve ardından aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="59e9b-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="59e9b-224">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="59e9b-225">12. adım: yapılandırma değerleri tooyour server.js dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="59e9b-226">Tooread oluşturduğunuz hello .config dosyası bu değerleri arasında uygulamamız ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="59e9b-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="59e9b-227">toodo bunu hello .config dosyası gerekli bir kaynak olarak bizim uygulamada ekleriz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="59e9b-228">Ardından hello genel değişkenler toomatch hello değişkenleri hello config.js belgede ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="59e9b-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="59e9b-229">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="59e9b-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="59e9b-230">Açık, `server.js` dosya, en sık kullandığınız düzenleyicide ve ardından aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="59e9b-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="59e9b-231">Yeni bir bölüm çok eklemek`server.js` koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="59e9b-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
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

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="59e9b-232">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="59e9b-233">13. adım: Mongoose kullanarak MongoDB Model ve şema bilgilerini hello Ekle</span><span class="sxs-lookup"><span data-stu-id="59e9b-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="59e9b-234">Şimdi bu hazırlık Biz bu üç dosyayı REST API hizmetinde birleştirmek gibi ödeme toostart geçiyor.</span><span class="sxs-lookup"><span data-stu-id="59e9b-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="59e9b-235">Bu kılavuz için 4. adımda açıklandığı gibi görevler MongoDB toostore kullanırız.</span><span class="sxs-lookup"><span data-stu-id="59e9b-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="59e9b-236">Merhaba, `config.js` dosya adım 11 oluşturduğumuz, biz Veritabanımıza adlı `tasklist`, biz hello sonuna eklediğiniz olduğu için bizim **mogoose_auth_local** bağlantı URL'si.</span><span class="sxs-lookup"><span data-stu-id="59e9b-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="59e9b-237">Bu veritabanında önceden MongoDB toocreate gerekmez.</span><span class="sxs-lookup"><span data-stu-id="59e9b-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="59e9b-238">Bunun yerine, MongoDB bu bize hello üzerinde ilk (Merhaba veritabanı önceden var olmayan varsayılarak) sunucu uygulamamız çalışma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="59e9b-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="59e9b-239">Biz hello sunucu hangi MongoDB veritabanını söylediyse göre toouse isteriz, toowrite bazı ek kod toocreate hello model ve şema bizim sunucunun görevler için ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="59e9b-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="59e9b-240">Merhaba modelinin tartışma</span><span class="sxs-lookup"><span data-stu-id="59e9b-240">Discussion of hello model</span></span>
<span data-ttu-id="59e9b-241">Bizim şema modeli basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-241">Our schema model is simple.</span></span> <span data-ttu-id="59e9b-242">Size gereken şekilde genişletin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-242">You expand it as required.</span></span>

<span data-ttu-id="59e9b-243">ADI: toohello göreve atanan hello kişi hello adı.</span><span class="sxs-lookup"><span data-stu-id="59e9b-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="59e9b-244">A **dize**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-244">A **String**.</span></span>

<span data-ttu-id="59e9b-245">: Hello görevi kendisi.</span><span class="sxs-lookup"><span data-stu-id="59e9b-245">TASK: hello task itself.</span></span> <span data-ttu-id="59e9b-246">A **dize**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-246">A **String**.</span></span>

<span data-ttu-id="59e9b-247">Tarihi: hello hello görev bitiş tarihidir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="59e9b-248">A **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-248">A **DATETIME**.</span></span>

<span data-ttu-id="59e9b-249">TAMAMLANAN: hello görev varsa veya tamamlanmış.</span><span class="sxs-lookup"><span data-stu-id="59e9b-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="59e9b-250">A **BOOLEAN**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="59e9b-251">Merhaba kodda Hello şema oluşturma</span><span class="sxs-lookup"><span data-stu-id="59e9b-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="59e9b-252">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="59e9b-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="59e9b-253">Açık, `server.js` en sık kullandığınız düzenleyicide dosya ve bilgileri hello yapılandırma girdisi altına aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="59e9b-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="59e9b-254">Merhaba koddan anlayabilirsiniz gibi bizim şema ilk oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="59e9b-255">Biz verilerimizi hello boyunca biz tanımlarken kod toostore kullandığımız bir model nesnesi oluşturup bizim **yollar**.</span><span class="sxs-lookup"><span data-stu-id="59e9b-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="59e9b-256">14. adım: bizim görev REST API sunucunuz için bizim yollar ekleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="59e9b-257">Veritabanı modeli toowork ile sahibiz, bizim REST API sunucunuz için devam eden kullanım duyuyoruz hello yollar ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="59e9b-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="59e9b-258">Restify'daki yollar hakkında</span><span class="sxs-lookup"><span data-stu-id="59e9b-258">About routes in Restify</span></span>
<span data-ttu-id="59e9b-259">Yollar iş Restify hello aynı bunlar hello Express yığın yolu.</span><span class="sxs-lookup"><span data-stu-id="59e9b-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="59e9b-260">Merhaba hello istemci uygulamaları toocall beklediğiniz URI kullanılarak yolları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="59e9b-261">Genellikle, yollarınızı ayrı bir dosyaya tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="59e9b-262">Bizim amacıyla, biz hello server.js dosyasında bizim yollar yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="59e9b-263">Üretim kullanımı için kendi dosyasına bu yollar faktörü öneririz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="59e9b-264">Bir Restify yolu için genel bir desen aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="59e9b-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="59e9b-265">Merhaba düzeni, en temel düzeyde budur.</span><span class="sxs-lookup"><span data-stu-id="59e9b-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="59e9b-266">Restify (ve hızlı) uygulama türlerini tanımlama ve farklı uç noktalar arasında karmaşık yönlendirme sağlama gibi çok daha kapsamlı işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e9b-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="59e9b-267">Bizim amacıyla, biz Bu yolları basit tutuyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="59e9b-268">Varsayılan yollar tooour sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-268">Add default routes tooour server</span></span>
<span data-ttu-id="59e9b-269">Biz şimdi hello temel CRUD yollarını oluşturma, alma, güncelleştirme, ekleme ve silme.</span><span class="sxs-lookup"><span data-stu-id="59e9b-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="59e9b-270">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasörü:</span><span class="sxs-lookup"><span data-stu-id="59e9b-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="59e9b-271">Açık hello `server.js` en sık kullandığınız düzenleyicide dosya ve bilgileri yaptığınız hello önceki veritabanı girişlerinin altına aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="59e9b-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

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
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="59e9b-272">Hata işleme bizim API'leri ekleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="59e9b-273">15. adım: sunucunuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="59e9b-273">Step 15: Create your server</span></span>
<span data-ttu-id="59e9b-274">Veritabanımıza tanımlamış olduğunuz ve bizim yollar yerdir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="59e9b-275">Merhaba son şey toodo bizim çağrıları yönetir hello sunucuyu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="59e9b-276">Restify'ı (ve hızlı) çok sayıda REST API sunucunuz için özelleştirme yapabilirsiniz ancak biz bizim amacıyla toouse hello en temel kurulumu tekrar kalacaklarını.</span><span class="sxs-lookup"><span data-stu-id="59e9b-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

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

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="59e9b-277">16. adım: hello yollar toohello sunucu (olmadan kimlik doğrulaması için şimdi) Ekle</span><span class="sxs-lookup"><span data-stu-id="59e9b-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="59e9b-278">17. adım: (OAuth desteğini eklemeden önce) hello sunucu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="59e9b-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="59e9b-279">Biz kimlik doğrulaması eklemeden önce sunucunuzu sınayın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="59e9b-280">Merhaba en kolay yolu tootest, komut satırında curl kullanarak, sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="59e9b-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="59e9b-281">Bunu önce bize tooparse çıktıyı JSON olarak sağlayan bir yardımcı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="59e9b-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="59e9b-282">JSON aracını (örnek tüm Merhaba, bu aracı kullanmak) aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="59e9b-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="59e9b-283">Bu hello JSON aracını Global olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="59e9b-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="59e9b-284">Şimdi biz elde, hello sunucusuyla Yürüt:</span><span class="sxs-lookup"><span data-stu-id="59e9b-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="59e9b-285">Öncelikle, mongoDB örneğinizin çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="59e9b-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="59e9b-286">Ardından, toohello dizini değiştirin ve curling başlatın:</span><span class="sxs-lookup"><span data-stu-id="59e9b-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="59e9b-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="59e9b-287">`$ cd azuread` `$ node server.js`</span></span>

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

4. <span data-ttu-id="59e9b-288">Ardından, biz bu şekilde bir görev ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="59e9b-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="59e9b-289">Merhaba yanıt şu şekilde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="59e9b-289">hello response should be:</span></span>

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
    <span data-ttu-id="59e9b-290">Ve şu görevleri bu şekilde Brandon için listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="59e9b-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="59e9b-291">Tüm bu çalışırsa, hazır tooadd OAuth toohello REST API sunucusuna çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="59e9b-292">Bir REST API MongoDB sunucusuyla var!</span><span class="sxs-lookup"><span data-stu-id="59e9b-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="59e9b-293">18. adım: kimlik doğrulaması tooour REST API sunucusuna ekleme</span><span class="sxs-lookup"><span data-stu-id="59e9b-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="59e9b-294">Çalışan bir REST API sahibiz, Azure AD ile yararlı hale getirme başlayalım.</span><span class="sxs-lookup"><span data-stu-id="59e9b-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="59e9b-295">Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.</span><span class="sxs-lookup"><span data-stu-id="59e9b-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="59e9b-296">Merhaba passport-azure-ad ile dahil edilen Oıdcbearerstrategy'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="59e9b-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="59e9b-297">Şu ana kadar herhangi türde bir yetkilendirme olmadan genel bir REST TODO sunucusu oluşturduğumuz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="59e9b-298">Burada, bir araya getirilmesi Başlat budur.</span><span class="sxs-lookup"><span data-stu-id="59e9b-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="59e9b-299">İlk olarak, toouse Passport istiyoruz tooindicate gerekir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="59e9b-300">Bu hak, diğer sunucu yapılandırmanızın sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="59e9b-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="59e9b-301">Ne zaman hello veri toosomething kullanıcı hello hello belirteçten benzersiz her zaman bağlantı öneririz API ' ları yazma taklit edilemez.</span><span class="sxs-lookup"><span data-stu-id="59e9b-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="59e9b-302">Bu sunucu, Yapılacaklar öğelerini depoladığında, bunları hello nesne kimliği, biz hello "sahip" alanına yerleştirin hello kullanıcının hello belirteçteki (token.oid denir) göre depolar.</span><span class="sxs-lookup"><span data-stu-id="59e9b-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="59e9b-303">Bu, yalnızca bu kullanıcının kendi TODOs erişebilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="59e9b-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="59e9b-304">Olmadığından hiçbir Etkilenme hello "sahip" API kimlikleri doğrulanır olsa bile bir dış kullanıcı hello diğer TODOs isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="59e9b-305">Sonraki birlikte hello taşıyıcı stratejisi kullanalım `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="59e9b-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="59e9b-306">Şu an için Hello koda bakın ve hello rest kısa süre içinde açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="59e9b-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="59e9b-307">Bu, ne yukarıda yapıştırdığınız sonra koyun:</span><span class="sxs-lookup"><span data-stu-id="59e9b-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
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

<span data-ttu-id="59e9b-308">Passport, strateji yazarlarının hepsinin bağlı tüm kendi stratejileri (Twitter, Facebook vb.) için benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="59e9b-309">Merhaba stratejisi baktığınızda, biz bir belirteç ve bir Bitti'yi olan bir işlev hello parametreler olarak geçirin bakın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="59e9b-310">kendi iş yaptıktan sonra hello stratejisi geri toous gelir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="59e9b-311">Bunu yaptıktan sonra biz tooask için yeniden gerekmez şekilde hello kullanıcı ve hazırlama hello belirteci depolarız.</span><span class="sxs-lookup"><span data-stu-id="59e9b-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59e9b-312">Merhaba önceki kod tooauthenticate tooour server olur herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="59e9b-313">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-313">This is known as auto-registration.</span></span> <span data-ttu-id="59e9b-314">Üretim sunucularında, herkesin bunları gerekmeden izin verme olduğunu öneririz karar kayıt işlemiyle gidin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="59e9b-315">Genellikle, Facebook ile tooregister ver, ancak ardından ek bilgi toofill isteyin tüketici uygulamalarında görürsünüz hello düzeni budur.</span><span class="sxs-lookup"><span data-stu-id="59e9b-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="59e9b-316">Bu komut satırı programı olmasaydı, biz hello e-posta döndürülen ve ek bilgiler hello kullanıcı toofill sorulan hello belirteç nesnesi ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="59e9b-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="59e9b-317">Bu bir test sunucusu olduğundan, biz bunları toohello bellek içi veritabanına eklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="59e9b-318">Bazı uç noktaları koruma</span><span class="sxs-lookup"><span data-stu-id="59e9b-318">Protect some endpoints</span></span>
<span data-ttu-id="59e9b-319">Merhaba belirterek uç noktaları koruma `passport.authenticate()` toouse istediğiniz çağrısı hello protokolü ile.</span><span class="sxs-lookup"><span data-stu-id="59e9b-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="59e9b-320">Bizim sunucu kodu yapmak bir şey daha fazla ilginç, toomake hello rota düzenlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="59e9b-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

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

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="59e9b-321">19. adım: sunucu uygulamanızı yeniden çalıştırın ve sizi reddettiğini olun</span><span class="sxs-lookup"><span data-stu-id="59e9b-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="59e9b-322">Kullanalım `curl` yeniden biz artık OAuth2 koruma bizim uç noktalarına karşı varsa toosee.</span><span class="sxs-lookup"><span data-stu-id="59e9b-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="59e9b-323">Biz, herhangi bir istemci SDK Bu uç noktaya karşı çalıştırmadan önce bu test yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59e9b-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="59e9b-324">Merhaba döndürülen üstbilgileri yeterli tootell olmalıdır bize doğru yolu hello yapacağız durumunda.</span><span class="sxs-lookup"><span data-stu-id="59e9b-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="59e9b-325">Öncelikle, mongoDB örneğinizin çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="59e9b-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="59e9b-326">Ardından, toohello dizini değiştirin ve curling başlatın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="59e9b-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="59e9b-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="59e9b-328">Temel bir POST deneyin.</span><span class="sxs-lookup"><span data-stu-id="59e9b-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="59e9b-329">Bir 401 burada aradığınız hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="59e9b-330">Bu yanıt hello Passport katman tooredirect toohello yetkili uç noktası, tam olarak ne olduğu çalışıyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59e9b-331">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59e9b-331">Next steps</span></span>
<span data-ttu-id="59e9b-332">OAuth2 uyumlu bir istemci kullanmadan bu sunucu ile kadar gitti.</span><span class="sxs-lookup"><span data-stu-id="59e9b-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="59e9b-333">Ek bir gözden geçirme aracılığıyla toogo gerekir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="59e9b-334">Bir REST API kullanarak nasıl tooimplement Restify artık öğrendiğinize ve OAuth2.</span><span class="sxs-lookup"><span data-stu-id="59e9b-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="59e9b-335">Ayrıca, hizmeti geliştirmek ve öğrenme birden fazla yeterli kod tookeep sahip nasıl toobuild Bu örnek üzerinde.</span><span class="sxs-lookup"><span data-stu-id="59e9b-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="59e9b-336">ADAL Yolculuğunuzun hello sonraki adımlarda ilgileniyorsanız, desteklenen bazı ADAL istemcileri ile çalışmaya devam öneririz aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="59e9b-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="59e9b-337">Tooyour Geliştirici makineyi kopyalama ve hello kılavuzda açıklandığı gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="59e9b-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="59e9b-338">İOS için ADAL</span><span class="sxs-lookup"><span data-stu-id="59e9b-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="59e9b-339">Android için ADAL</span><span class="sxs-lookup"><span data-stu-id="59e9b-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
