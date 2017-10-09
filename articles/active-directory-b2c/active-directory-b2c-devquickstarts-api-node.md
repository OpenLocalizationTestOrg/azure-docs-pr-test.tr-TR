---
title: "Azure AD B2C: Node.js kullanarak bir web API'sinin güvenliğini sağlama | Microsoft Belgeleri"
description: "Toobuild bir Node.js web nasıl API B2C kiracısından belirteç kabul eden"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="9df81-103">Azure AD B2C: Node.js kullanarak bir web API'sinin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="9df81-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="9df81-104">Azure Active Directory (Azure AD) B2C ile OAuth 2.0 erişim belirteçleri kullanarak web API'si güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9df81-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="9df81-105">Bu belirteçler Azure AD B2C tooauthenticate toohello API kullanan istemci uygulamalarınızın izin verir.</span><span class="sxs-lookup"><span data-stu-id="9df81-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="9df81-106">Bu makalede nasıl toocreate bir "Yapılacaklar listesi" API kullanıcılar tooadd ve liste görevleri sağlayan gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9df81-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="9df81-107">Merhaba web API'sini Azure AD B2C kullanarak güvenli ve kimliği doğrulanmış kullanıcılar toomanage kendi Yapılacaklar listesi yalnızca sağlar.</span><span class="sxs-lookup"><span data-stu-id="9df81-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="9df81-108">Bu örnek tooby bağlı toobe kullanılarak yazılmıştır bizim [iOS B2C örnek uygulamamızı](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="9df81-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="9df81-109">Geçerli gözden geçirme ilk hello ve o örneği takip edin.</span><span class="sxs-lookup"><span data-stu-id="9df81-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="9df81-110">**Passport**, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="9df81-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="9df81-111">Esnek ve modüler özellikteki Passport, Express tabanlı veya Restify web uygulamasına sorunsuz bir şekilde yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="9df81-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="9df81-112">Bir dizi kapsamlı strateji; bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="9df81-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="9df81-113">Azure Active Directory (Azure AD) için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="9df81-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9df81-114">Bu modülü yükleyin ve ardından hello Azure AD ekleyin `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="9df81-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="9df81-115">toodo Bu örnek, gerekir:</span><span class="sxs-lookup"><span data-stu-id="9df81-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="9df81-116">Bir uygulamayı Azure AD'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9df81-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="9df81-117">Uygulama toouse Passport's ayarlamak `azure-ad-passport` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="9df81-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="9df81-118">İstemci uygulama toocall hello "Yapılacaklar listesi" web API'si yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9df81-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="9df81-119">Azure AD B2C dizini alma</span><span class="sxs-lookup"><span data-stu-id="9df81-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="9df81-120">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9df81-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="9df81-121">Dizin; tüm kullanıcılar, uygulamalar, gruplar ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="9df81-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="9df81-122">Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9df81-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="9df81-123">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="9df81-123">Create an application</span></span>
<span data-ttu-id="9df81-124">Ardından B2C dizininizde Azure AD toosecurely gereken bazı bilgiler sağlayan bir uygulamanın iletişim toocreate uygulamanızla gerekir.</span><span class="sxs-lookup"><span data-stu-id="9df81-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="9df81-125">Bu durumda, hem hello istemci uygulaması hem de web API'si tarafından tek bir temsil edilir **uygulama kimliği**, bir mantıksal uygulama içerdikleri için.</span><span class="sxs-lookup"><span data-stu-id="9df81-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="9df81-126">Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="9df81-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="9df81-127">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="9df81-127">Be sure to:</span></span>

* <span data-ttu-id="9df81-128">Dahil bir **web uygulaması/web API** hello uygulamada</span><span class="sxs-lookup"><span data-stu-id="9df81-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="9df81-129">**Yanıt URL'si** olarak `http://localhost/TodoListService` adresini girin.</span><span class="sxs-lookup"><span data-stu-id="9df81-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="9df81-130">Bu kod örneği için hello varsayılan URL değil.</span><span class="sxs-lookup"><span data-stu-id="9df81-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="9df81-131">Uygulamanız için bir **Uygulama gizli anahtarı** oluşturun ve bunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9df81-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="9df81-132">Bu veriler daha sonra gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9df81-132">You need this data later.</span></span> <span data-ttu-id="9df81-133">Bu değer toobe gerektiğini Not [XML kaçışlı](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) kullanmadan önce.</span><span class="sxs-lookup"><span data-stu-id="9df81-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="9df81-134">Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="9df81-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="9df81-135">Bu veriler daha sonra gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9df81-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="9df81-136">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9df81-136">Create your policies</span></span>
<span data-ttu-id="9df81-137">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9df81-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="9df81-138">Bu uygulama iki kimlik deneyimi içerir: kaydolma ve oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9df81-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="9df81-139">Bölümünde açıklandığı gibi her tür bir ilke toocreate gerek [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="9df81-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="9df81-140">Üç ilkenizi oluştururken şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="9df81-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="9df81-141">Merhaba seçin **görünen adı** ve diğer kaydolma özniteliklerini kaydolma ilkenizde.</span><span class="sxs-lookup"><span data-stu-id="9df81-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="9df81-142">Merhaba seçin **görünen adı** ve **nesne kimliği** her ilkede uygulamanın talep.</span><span class="sxs-lookup"><span data-stu-id="9df81-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="9df81-143">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9df81-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="9df81-144">Merhaba basılı kopya **adı** oluşturduktan sonra her ilkenin.</span><span class="sxs-lookup"><span data-stu-id="9df81-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="9df81-145">Merhaba önekine sahip olmalıdır `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="9df81-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="9df81-146">Bu ilke adları daha sonra gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9df81-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="9df81-147">Üç ilkenizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="9df81-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="9df81-148">toolearn ile Merhaba ilkelerinin Azure AD B2C'de nasıl çalıştığı hakkında başlangıç [.NET web uygulamasıyla çalışmaya başlama Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9df81-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="9df81-149">Merhaba kodu indirme</span><span class="sxs-lookup"><span data-stu-id="9df81-149">Download hello code</span></span>
<span data-ttu-id="9df81-150">Bu öğretici için kod Hello [Github'da korunur](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="9df81-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="9df81-151">toobuild hello örnek olarak, Git, yapabilecekleriniz [çatı projesini .zip dosyası olarak indirebilirsiniz](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="9df81-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="9df81-152">Ayrıca hello çatıyı kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9df81-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="9df81-153">Tamamlanan hello uygulamadır de [.zip dosyası olarak kullanılabilir](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) veya hello `complete` hello dalı aynı deposu.</span><span class="sxs-lookup"><span data-stu-id="9df81-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="9df81-154">Platformunuz için Node.js indirme</span><span class="sxs-lookup"><span data-stu-id="9df81-154">Download Node.js for your platform</span></span>
<span data-ttu-id="9df81-155">Bu örnek toosuccessfully kullanın, Node.js çalışan yüklemesine gerekir.</span><span class="sxs-lookup"><span data-stu-id="9df81-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="9df81-156">[nodejs.org](http://nodejs.org) adresinden Node.js'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9df81-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="9df81-157">Platformunuz için MongoDB yükleme</span><span class="sxs-lookup"><span data-stu-id="9df81-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="9df81-158">toosuccessfully kullanın Bu örnek, MongoDB çalışan yüklemesine gerekir.</span><span class="sxs-lookup"><span data-stu-id="9df81-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="9df81-159">MongoDB toomake kalıcı, REST API'nizi sunucu örneklerinde kullanırız.</span><span class="sxs-lookup"><span data-stu-id="9df81-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="9df81-160">[mongodb.org](http://www.mongodb.org) adresinden MongoDB'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9df81-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="9df81-161">Bu kılavuz hello varsayılan yükleme ve sunucu uç noktaları olan bu yazma hello zamanında MongoDB kullanmak varsayar `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="9df81-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="9df81-162">Merhaba Restify modüllerini web API'nize yükleme</span><span class="sxs-lookup"><span data-stu-id="9df81-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="9df81-163">REST API'nizi Restify toobuild kullanırız.</span><span class="sxs-lookup"><span data-stu-id="9df81-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="9df81-164">Restify, Express'ten türetilen minimal ve esnek bir Node.js uygulama çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="9df81-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="9df81-165">Connect üstünde REST API'leri oluşturmaya yönelik bir dizi sağlam özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9df81-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="9df81-166">Restify'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="9df81-166">Install Restify</span></span>
<span data-ttu-id="9df81-167">Merhaba komut satırından dizininizi çok değiştirin`azuread`.</span><span class="sxs-lookup"><span data-stu-id="9df81-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="9df81-168">Merhaba, `azuread` dizin mevcut değil, oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9df81-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="9df81-169">`cd azuread` veya `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="9df81-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="9df81-170">Merhaba aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="9df81-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="9df81-171">Bu komut Restify'ı yükler.</span><span class="sxs-lookup"><span data-stu-id="9df81-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="9df81-172">Hata mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="9df81-172">Did you get an error?</span></span>
<span data-ttu-id="9df81-173">Bazı işletim sistemlerindeki kullandığınızda, `npm`, hello hata iletisini alabilirsiniz `Error: EPERM, chmod '/usr/local/bin/..'` ve bir istek hello hesabı yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9df81-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="9df81-174">Bu sorun oluşursa, hello kullan `sudo` komutu toorun `npm` daha yüksek bir ayrıcalık düzeyinde.</span><span class="sxs-lookup"><span data-stu-id="9df81-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="9df81-175">Bir DTrace hatası mı aldınız?</span><span class="sxs-lookup"><span data-stu-id="9df81-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="9df81-176">Restify'ı yüklediğinizde şöyle bir metin görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9df81-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="9df81-177">Restify, DTrace kullanarak REST çağrılarını izlemek için güçlü bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="9df81-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="9df81-178">Ancak çoğu işletim sisteminde DTrace kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="9df81-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="9df81-179">Bu hataları güvenle yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9df81-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="9df81-180">Merhaba hello komutunun çıkışını benzer toothis metin görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="9df81-180">hello output of hello command should appear similar toothis text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="9df81-181">Passport'u web API'nize yükleme</span><span class="sxs-lookup"><span data-stu-id="9df81-181">Install Passport in your web API</span></span>
<span data-ttu-id="9df81-182">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="9df81-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="9df81-183">Passport komutu aşağıdaki hello kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9df81-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="9df81-184">Merhaba hello komutunun çıkışını benzer toothis metin olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="9df81-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="9df81-185">Passport-azuread'i tooyour web API ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="9df81-186">Ardından, kullanarak hello OAuth stratejisini ekleyin `passport-azuread`, Azure AD'yi Passport'a bağlayan stratejileri dizisi.</span><span class="sxs-lookup"><span data-stu-id="9df81-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="9df81-187">Merhaba REST API'si örneğindeki taşıyıcı belirteçler için bu stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="9df81-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="9df81-188">OAuth2, herhangi bir bilinen belirteç türünün verilebileceği bir altyapı sağlasa da yalnızca belirli belirteç türleri yaygın kullanım elde etmiştir.</span><span class="sxs-lookup"><span data-stu-id="9df81-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="9df81-189">uç noktaları korumaya hello belirteçler, taşıyıcı belirteçlerdir.</span><span class="sxs-lookup"><span data-stu-id="9df81-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="9df81-190">Bu belirteçler OAuth2 en yaygın olarak verilen hello türleridir.</span><span class="sxs-lookup"><span data-stu-id="9df81-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="9df81-191">Birçok uygulama, taşıyıcı belirteçlerini hello tek belirteç türü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="9df81-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="9df81-192">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="9df81-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="9df81-193">Merhaba Passport yüklemek `passport-azure-ad` komutu aşağıdaki hello kullanarak Modülü:</span><span class="sxs-lookup"><span data-stu-id="9df81-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="9df81-194">Merhaba hello komutunun çıkışını benzer toothis metin olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="9df81-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="9df81-195">MongoDB modülleri tooyour web API ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="9df81-196">Bu örnekte MongoDB veri deponuz olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9df81-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="9df81-197">Bunun için modelleri ve şemaları yönetmeye yönelik yaygın kullanılan bir eklenti olan Mongoose’u yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9df81-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="9df81-198">Ek modüller yükleme</span><span class="sxs-lookup"><span data-stu-id="9df81-198">Install additional modules</span></span>
<span data-ttu-id="9df81-199">Ardından, kalan gerekli modüllerini hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9df81-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="9df81-200">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:</span><span class="sxs-lookup"><span data-stu-id="9df81-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="9df81-201">Merhaba modüllerini yüklemek, `node_modules` dizini:</span><span class="sxs-lookup"><span data-stu-id="9df81-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="9df81-202">Bağımlılıklarınız ile bir server.js dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9df81-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="9df81-203">Merhaba `server.js` dosyası, Web API sunucunuz için hello işlevselliği hello çoğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="9df81-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="9df81-204">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:</span><span class="sxs-lookup"><span data-stu-id="9df81-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="9df81-205">Bir düzenleyicide `server.js` dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9df81-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="9df81-206">Aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9df81-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="9df81-207">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9df81-207">Save hello file.</span></span> <span data-ttu-id="9df81-208">Tooit daha sonra geri dönün.</span><span class="sxs-lookup"><span data-stu-id="9df81-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="9df81-209">Azure AD ayarlarınızı bir config.js dosyası toostore oluşturma</span><span class="sxs-lookup"><span data-stu-id="9df81-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="9df81-210">Bu kod dosyası, Azure AD portalı toohello hello yapılandırma parametrelerini geçirir `Passport.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="9df81-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="9df81-211">Merhaba ilk hello gözden geçirme bölümünde hello web API toohello portal eklendiğinde bu yapılandırma değerlerini oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="9df81-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="9df81-212">Merhaba kodu kopyaladıktan sonra biz hello değerleri bu parametre hangi tooput açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9df81-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="9df81-213">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:</span><span class="sxs-lookup"><span data-stu-id="9df81-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="9df81-214">Bir düzenleyicide `config.js` dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9df81-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="9df81-215">Aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9df81-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="9df81-216">Gerekli değerler</span><span class="sxs-lookup"><span data-stu-id="9df81-216">Required values</span></span>
<span data-ttu-id="9df81-217">`clientID`: Merhaba Web API uygulamanızın istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="9df81-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="9df81-218">`IdentityMetadata`: Bu yerdir `passport-azure-ad` hello kimlik sağlayıcısı için yapılandırma verilerinizi arar.</span><span class="sxs-lookup"><span data-stu-id="9df81-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="9df81-219">Ayrıca, hello anahtarları toovalidate hello JSON web belirteçlerini için arar.</span><span class="sxs-lookup"><span data-stu-id="9df81-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="9df81-220">`audience`: Merhaba, çağıran uygulama tanımlayan hello portalından Tekdüzen Kaynak Tanımlayıcısı (URI).</span><span class="sxs-lookup"><span data-stu-id="9df81-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="9df81-221">`tenantName`: Kiracı adınız (örneğin, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="9df81-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="9df81-222">`policyName`: Merhaba tooyour Server'da gelen toovalidate hello belirteçleri istediğiniz ilke.</span><span class="sxs-lookup"><span data-stu-id="9df81-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="9df81-223">Bu ilke olmalıdır hello hello istemci uygulaması oturum açmak için kullandığınız aynı ilke.</span><span class="sxs-lookup"><span data-stu-id="9df81-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="9df81-224">Şimdilik, kullanım hello aynı istemci ve sunucu kurulumunda arasında ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="9df81-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="9df81-225">Zaten bir gözden geçirme tamamlandı ve bu ilkeleri oluşturduysanız, bu nedenle yeniden toodo gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9df81-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="9df81-226">Merhaba Kılavuzu tamamladığınız hello sitede istemci kılavuzlarına yönelik yeni ilkeleri tooset gerek döndürmemelidir.</span><span class="sxs-lookup"><span data-stu-id="9df81-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="9df81-227">Yapılandırma tooyour server.js dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="9df81-228">Merhaba tooread hello değerleri `config.js` oluşturduğunuz dosya, hello eklemek `.config` dosya uygulamanızda gerekli bir kaynak olarak ve ardından hello hello genel değişkenler toothose `config.js` belge.</span><span class="sxs-lookup"><span data-stu-id="9df81-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="9df81-229">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:</span><span class="sxs-lookup"><span data-stu-id="9df81-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="9df81-230">Açık hello `server.js` dosyasına bir düzenleyicide.</span><span class="sxs-lookup"><span data-stu-id="9df81-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="9df81-231">Aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9df81-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="9df81-232">Yeni bir bölüm çok eklemek`server.js` koddan hello içerir:</span><span class="sxs-lookup"><span data-stu-id="9df81-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="9df81-233">Ardından, arama bizim uygulamalardan aldığımız hello kullanıcılar için bazı yer tutucuları ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="9df81-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="9df81-234">Devam edip günlükçümüzü de oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="9df81-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="9df81-235">Mongoose kullanarak Hello MongoDB model ve şema bilgilerini ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="9df81-236">Bu üç dosyayı REST API hizmetinde araya getirdiğiniz hello erken hazırlık ödeyen devre dışı.</span><span class="sxs-lookup"><span data-stu-id="9df81-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="9df81-237">Bu kılavuz, MongoDB toostore daha önce bahsedildiği gibi görevlerinizin kullanın.</span><span class="sxs-lookup"><span data-stu-id="9df81-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="9df81-238">Merhaba, `config.js` dosyası, veritabanınızı adlı **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="9df81-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="9df81-239">Bu ayrıca hello hello sonuna eklediğiniz adlandırılmıştı `mongoose_auth_local` bağlantı URL'si.</span><span class="sxs-lookup"><span data-stu-id="9df81-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="9df81-240">Bu veritabanında önceden MongoDB toocreate gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9df81-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="9df81-241">Merhaba veritabanı sizin için hello ilk sunucu uygulamanızı çalıştırılmasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9df81-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="9df81-242">Hangi MongoDB veritabanı toouse hello sunucusuna bildirmek sonra toowrite bazı ek kod toocreate hello model ve şema sunucu görevleriniz için gerekir.</span><span class="sxs-lookup"><span data-stu-id="9df81-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="9df81-243">Merhaba modeli genişletme</span><span class="sxs-lookup"><span data-stu-id="9df81-243">Expand hello model</span></span>
<span data-ttu-id="9df81-244">Bu şema modeli basittir.</span><span class="sxs-lookup"><span data-stu-id="9df81-244">This schema model is simple.</span></span> <span data-ttu-id="9df81-245">Gerektiği şekilde genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9df81-245">You can expand it as required.</span></span>

<span data-ttu-id="9df81-246">`owner`: Göreve toohello görev atanır.</span><span class="sxs-lookup"><span data-stu-id="9df81-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="9df81-247">Bu nesne bir **string**.</span><span class="sxs-lookup"><span data-stu-id="9df81-247">This object is a **string**.</span></span>  

<span data-ttu-id="9df81-248">`Text`: hello görevin kendisi.</span><span class="sxs-lookup"><span data-stu-id="9df81-248">`Text`: hello task itself.</span></span> <span data-ttu-id="9df81-249">Bu nesne bir **string**.</span><span class="sxs-lookup"><span data-stu-id="9df81-249">This object is a **string**.</span></span>

<span data-ttu-id="9df81-250">`date`: Başlangıç tarihi bu hello son bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="9df81-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="9df81-251">Bu nesne bir **datetime**.</span><span class="sxs-lookup"><span data-stu-id="9df81-251">This object is a **datetime**.</span></span>

<span data-ttu-id="9df81-252">`completed`: Başlangıç görevi ise tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="9df81-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="9df81-253">Bu nesne bir **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="9df81-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="9df81-254">Merhaba kodda Hello şema oluşturun</span><span class="sxs-lookup"><span data-stu-id="9df81-254">Create hello schema in hello code</span></span>
<span data-ttu-id="9df81-255">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:</span><span class="sxs-lookup"><span data-stu-id="9df81-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="9df81-256">Açık hello `server.js` dosyasına bir düzenleyicide.</span><span class="sxs-lookup"><span data-stu-id="9df81-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="9df81-257">Hello aşağıdaki bilgilerle hello yapılandırma girdisi altına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9df81-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="9df81-258">İlk hello şema oluşturun ve ardından hello genelindeki verilerinizi tanımlarken kod toostore kullanan bir model nesnesi oluşturun, **yollar**.</span><span class="sxs-lookup"><span data-stu-id="9df81-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="9df81-259">REST API görev sunucunuz için yollar ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="9df81-260">Veritabanı modeli toowork ile sahip olduğunuza göre REST API sunucunuz için kullandığınız hello yolları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9df81-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="9df81-261">Restify'daki yollar hakkında</span><span class="sxs-lookup"><span data-stu-id="9df81-261">About routes in Restify</span></span>
<span data-ttu-id="9df81-262">Yollar iş Restify'da hello aynı hello Express yığınını kullandıklarında çalıştıkları şekilde.</span><span class="sxs-lookup"><span data-stu-id="9df81-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="9df81-263">Merhaba hello istemci uygulamaları toocall beklediğiniz URI kullanılarak yolları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9df81-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="9df81-264">Bir Restify yolu için genel bir desen:</span><span class="sxs-lookup"><span data-stu-id="9df81-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="9df81-265">Restify ve Express, uygulama türlerini tanımlama ve farklı uç noktalar arasında karmaşık yönlendirme yapma gibi çok daha kapsamlı işlevsellik sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="9df81-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="9df81-266">Bu öğreticinin Hello amaçları doğrultusunda, biz Bu yolları basit tutun.</span><span class="sxs-lookup"><span data-stu-id="9df81-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="9df81-267">Varsayılan yollar tooyour sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-267">Add default routes tooyour server</span></span>
<span data-ttu-id="9df81-268">Şimdi hello temel CRUD yollarını ekleyin **oluşturma** ve **listesi** bizim REST API için.</span><span class="sxs-lookup"><span data-stu-id="9df81-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="9df81-269">Diğer yollar hello bulunabilir `complete` hello örnek dalı.</span><span class="sxs-lookup"><span data-stu-id="9df81-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="9df81-270">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:</span><span class="sxs-lookup"><span data-stu-id="9df81-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="9df81-271">Açık hello `server.js` dosyasına bir düzenleyicide.</span><span class="sxs-lookup"><span data-stu-id="9df81-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="9df81-272">Merhaba veritabanı girişlerinin aşağıdaki bilgilerle hello yukarıdaki Ekle yaptığınız:</span><span class="sxs-lookup"><span data-stu-id="9df81-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="9df81-273">Merhaba yollar için hata işleme ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-273">Add error handling for hello routes</span></span>
<span data-ttu-id="9df81-274">Anlayabileceği bir şekilde geri toohello istemci karşılaştığınız sorunları iletişim kurabilmesi için bazı hata işleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9df81-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="9df81-275">Hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9df81-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="9df81-276">Sunucunuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9df81-276">Create your server</span></span>
<span data-ttu-id="9df81-277">Artık veritabanınızı tanımladınız ve yollarınızı yerleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="9df81-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="9df81-278">Merhaba son, toodo için çağrılarınızı yönetmediğinden tooadd hello sunucu örneği şeydir.</span><span class="sxs-lookup"><span data-stu-id="9df81-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="9df81-279">Restify ve Express REST API sunucunuz için kapsamlı özelleştirme sağlar ancak burada kullandığımız hello en temel kurulumu.</span><span class="sxs-lookup"><span data-stu-id="9df81-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="9df81-280">Merhaba yollar toohello sunucu (kimlik doğrulaması olmadan) ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="9df81-281">Kimlik doğrulama tooyour REST API sunucusu ekleme</span><span class="sxs-lookup"><span data-stu-id="9df81-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="9df81-282">Artık çalışan bir REST API sunucunuz olduğuna göre bunu Azure AD için faydalı hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9df81-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="9df81-283">Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:</span><span class="sxs-lookup"><span data-stu-id="9df81-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="9df81-284">Merhaba passport-azure-ad ile dahil edilen Oıdcbearerstrategy'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="9df81-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="9df81-285">Ne zaman hello veri toosomething kullanıcı hello hello belirteçten benzersiz her zaman bağlanması gereken API ' ları yazma taklit edilemez.</span><span class="sxs-lookup"><span data-stu-id="9df81-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="9df81-286">Merhaba sunucu Yapılacaklar öğelerini depoladığında hello böylece göre mu **OID** hangi hello "sahip" alanına hello kullanıcının hello belirteçteki (token.oid denir).</span><span class="sxs-lookup"><span data-stu-id="9df81-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="9df81-287">Bu değer kendi ToDo öğesine yalnızca bu kullanıcının erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9df81-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="9df81-288">Olmadığından hiçbir Etkilenme hello "sahip" API bir dış kullanıcı kimlikleri doğrulanır olsa bile başkalarının Yapılacaklar öğelerini isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="9df81-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="9df81-289">Ardından, birlikte hello taşıyıcı stratejisi kullanın `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="9df81-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="9df81-290">Passport, tüm stratejileri hello aynı desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="9df81-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="9df81-291">Bu desene, parametre olarak `token` ve `done` öğelerini barındıran bir `function()` geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9df81-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="9df81-292">tüm işlemlerini tamamladıktan sonra hello stratejisi tooyou gelir.</span><span class="sxs-lookup"><span data-stu-id="9df81-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="9df81-293">Ardından hello kullanıcı depolamak ve gerekir hello belirteci kaydetmek için yeniden tooask gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9df81-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9df81-294">Yukarıdaki Hello kod tooauthenticate tooyour server olur herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="9df81-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="9df81-295">Bu işlem otomatik kayıt olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="9df81-295">This process is known as autoregistration.</span></span> <span data-ttu-id="9df81-296">Üretim sunucularında, bunları bir kayıt sürecinden geçerler gerekmeden tüm kullanıcılara erişim hello API izin vermeyin.</span><span class="sxs-lookup"><span data-stu-id="9df81-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="9df81-297">Bu genellikle, Facebook kullanarak tooregister izin ver, ancak ardından ek bilgi toofill isteyin tüketici uygulamalarında görürsünüz hello düzeni işlemidir.</span><span class="sxs-lookup"><span data-stu-id="9df81-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="9df81-298">Bu programın komut satırı programı olmasaydı, biz hello e-posta döndürülen ve ek bilgiler kullanıcıların toofill sorulan hello belirteç nesnesi ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="9df81-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="9df81-299">Bu bir örnek olduğundan, bunları tooan bellek içi veritabanına ekleriz.</span><span class="sxs-lookup"><span data-stu-id="9df81-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="9df81-300">Sunucu uygulaması tooverify çalıştırmak, BT'nin sizi reddettiğini</span><span class="sxs-lookup"><span data-stu-id="9df81-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="9df81-301">Kullanabileceğiniz `curl` artık uç noktalarınızda OAuth2 koruması varsa toosee.</span><span class="sxs-lookup"><span data-stu-id="9df81-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="9df81-302">Merhaba döndürülen üstbilgileri yeterli tootell olmalıdır hello doğru yolda olduğunu.</span><span class="sxs-lookup"><span data-stu-id="9df81-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="9df81-303">MongoDB örneğinizin çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="9df81-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="9df81-304">Toohello dizin ve çalışma hello sunucu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9df81-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="9df81-305">Yeni bir terminal penceresinde şunu çalıştırın: `curl`</span><span class="sxs-lookup"><span data-stu-id="9df81-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="9df81-306">Temel bir POST deneyin:</span><span class="sxs-lookup"><span data-stu-id="9df81-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="9df81-307">Merhaba yanıt istediğiniz bir 401 hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="9df81-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="9df81-308">Merhaba Passport katman tooredirect çalışıyor gösterir toohello kimlik doğrulama uç noktası.</span><span class="sxs-lookup"><span data-stu-id="9df81-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="9df81-309">Artık OAuth2 kullanan bir REST API'niz var</span><span class="sxs-lookup"><span data-stu-id="9df81-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="9df81-310">Restify ve OAuth kullanarak bir REST API’si uyguladık!</span><span class="sxs-lookup"><span data-stu-id="9df81-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="9df81-311">Böylece hizmetinizi toodevelop devam ve bu örneği temel yapı artık gerekli koda sahip.</span><span class="sxs-lookup"><span data-stu-id="9df81-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="9df81-312">OAuth2 uyumlu bir istemci kullanmadan bu sunucu ile çalışabildiğiniz kadar çalıştınız.</span><span class="sxs-lookup"><span data-stu-id="9df81-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="9df81-313">İlave bir kılavuz gibi bir sonraki adımda kullanmak bizim [tooa web API B2C ile iOS kullanarak bağlanmak](active-directory-b2c-devquickstarts-ios.md) gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="9df81-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9df81-314">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9df81-314">Next steps</span></span>
<span data-ttu-id="9df81-315">Gelişmiş toomore konuları gibi geçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9df81-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="9df81-316">Tooa web API B2C ile iOS kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="9df81-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
