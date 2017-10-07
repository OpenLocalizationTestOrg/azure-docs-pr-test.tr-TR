---
title: "aaaAzure AD Başlarken Cordova | Microsoft Docs"
description: "Nasıl toobuild bir Cordova uygulaması, oturum açma için Azure AD ile tümleşir ve OAuth kullanarak Azure AD korumalı API'lerini çağırır."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="296b0-103">Azure AD tümleştirme bir Apache Cordova uygulaması</span><span class="sxs-lookup"><span data-stu-id="296b0-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="296b0-104">Mobil aygıtlarda tam özellikli yerel uygulamalar olarak çalıştırabilirsiniz Apache Cordova toodevelop HTML5/JavaScript uygulamaları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="296b0-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="296b0-105">Azure Active Directory ile (Azure AD), kurumsal düzeyde kimlik doğrulama özellikleri tooyour Cordova uygulamaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="296b0-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="296b0-106">Cordova eklentisi Azure sarmalar AD yerel SDK'ları iOS, Android, Windows mağazası ve Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="296b0-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="296b0-107">Eklenti, uygulamanızın geliştirebilirsiniz olduğunu kullanarak toosupport kullanıcılarınızın Windows Server Active Directory hesapları, kazanç erişim tooOffice 365 ve Azure API'leri ile oturum açma ve hatta korunmasına yardımcı olur çağrıları tooyour kendi özel web API.</span><span class="sxs-lookup"><span data-stu-id="296b0-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="296b0-108">Bu öğreticide, hello Apache Cordova eklentisi Active Directory Authentication Library (ADAL) tooimprove basit bir uygulama için özellikler aşağıdaki hello ekleyerek kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="296b0-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="296b0-109">Yalnızca birkaç satır kod ile bir kullanıcının kimliğini doğrulamak ve bir belirteç elde edin.</span><span class="sxs-lookup"><span data-stu-id="296b0-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="296b0-110">Merhaba sonuçlarını görüntülemek ve bu dizine, belirteç tooinvoke hello grafik API'si tooquery kullanın.</span><span class="sxs-lookup"><span data-stu-id="296b0-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="296b0-111">Merhaba ADAL belirteç önbelleği toominimize kimlik doğrulamasını kullan hello kullanıcıya sorar.</span><span class="sxs-lookup"><span data-stu-id="296b0-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="296b0-112">toomake Bu geliştirmeler, gerekir:</span><span class="sxs-lookup"><span data-stu-id="296b0-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="296b0-113">Bir uygulamayı Azure AD'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="296b0-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="296b0-114">Kod tooyour uygulama toorequest belirteçleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="296b0-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="296b0-115">Merhaba grafik API'si sorgulanırken kod toouse hello belirteci ekleyin ve sonuçları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="296b0-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="296b0-116">Merhaba Cordova dağıtım projesi oluşturmak tüm hello platformlarında, tootarget istediğiniz, hello Cordova ADAL eklenti ekleme ve test hello çözüm içinde Öykünücüler.</span><span class="sxs-lookup"><span data-stu-id="296b0-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="296b0-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="296b0-117">Prerequisites</span></span>
<span data-ttu-id="296b0-118">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="296b0-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="296b0-119">Uygulama geliştirme hakları olan bir hesabın sahip olduğu bir Azure AD kiracısı.</span><span class="sxs-lookup"><span data-stu-id="296b0-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="296b0-120">Apache Cordova toouse yapılandırmış bir geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="296b0-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="296b0-121">Her ikisi de varsa, ayarlamak, doğrudan toostep 1 devam edin.</span><span class="sxs-lookup"><span data-stu-id="296b0-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="296b0-122">Azure AD kiracısı yoksa, hello kullan [yönergeler tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="296b0-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="296b0-123">Apache Cordova makinenizde ayarlanan yoksa, hello aşağıdakileri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="296b0-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="296b0-124">Git</span><span class="sxs-lookup"><span data-stu-id="296b0-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="296b0-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="296b0-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="296b0-126">[Cordova CLI](https://cordova.apache.org/) (NPM Paket Yöneticisi kolayca yüklenebilir: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="296b0-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="296b0-127">yüklemeleri önceki hello hello PC ve Mac hello çalışması gerekir</span><span class="sxs-lookup"><span data-stu-id="296b0-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="296b0-128">Her hedef platformu farklı Önkoşullar vardır:</span><span class="sxs-lookup"><span data-stu-id="296b0-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="296b0-129">toobuild ve Windows Tablet/PC veya Windows Phone için uygulama çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="296b0-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="296b0-130">Yükleme [Windows Update 2 veya sonraki sürümü için Visual Studio 2013](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express veya başka bir sürümü) veya [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="296b0-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="296b0-131">toobuild ve iOS için uygulama çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="296b0-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="296b0-132">Xcode yükleme 6.x veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="296b0-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="296b0-133">Hello karşıdan [Apple Developer site](http://developer.apple.com/downloads) veya hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="296b0-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="296b0-134">Yükleme [ios-SIM](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="296b0-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="296b0-135">İOS simülatörü hello komut satırından içinde toostart iOS uygulamalarını bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="296b0-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="296b0-136">(Kolayca hello terminal yükleyebilirsiniz: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="296b0-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="296b0-137">toobuild ve Android için uygulama çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="296b0-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="296b0-138">Yükleme [Java Geliştirme Seti (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="296b0-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="296b0-139">Emin olun `JAVA_HOME` (ortam değişkeni), toohello JDK yükleme yolu (örneğin, C:\Program Files\Java\jdk1.7.0_75) göre doğru şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="296b0-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="296b0-140">Yükleme [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) ve hello ekleyin `<android-sdk-location>\tools` konum (örneğin, C:\tools\Android\android-sdk\tools) tooyour `PATH` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="296b0-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="296b0-141">Android SDK Yöneticisi'ni açın (örneğin, terminal hello aracılığıyla: `android`) ve yükleyin:</span><span class="sxs-lookup"><span data-stu-id="296b0-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="296b0-142">*Android 5.0.1 (API 21)* platform SDK'si</span><span class="sxs-lookup"><span data-stu-id="296b0-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="296b0-143">*Android SDK derleme araçlarını* sürüm 19.1.0 veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="296b0-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="296b0-144">*Android desteği depo* (ek özellikler)</span><span class="sxs-lookup"><span data-stu-id="296b0-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="296b0-145">Merhaba Android SDK varsayılan öykünücü örnek sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="296b0-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="296b0-146">Çalıştırarak oluşturmak `android avd` hello terminal ve ardından seçerek **oluşturma**toorun hello Android uygulamasını bir öykünücü istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="296b0-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="296b0-147">19 veya daha yüksek bir API düzeyi öneririz.</span><span class="sxs-lookup"><span data-stu-id="296b0-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="296b0-148">Merhaba Android öykünücü ve oluşturma seçenekleri hakkında daha fazla bilgi için bkz: [AVD Yöneticisi](http://developer.android.com/tools/help/avd-manager.html) hello Android sitesinde.</span><span class="sxs-lookup"><span data-stu-id="296b0-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="296b0-149">1. adım: bir uygulamayı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="296b0-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="296b0-150">Bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="296b0-150">This step is optional.</span></span> <span data-ttu-id="296b0-151">Bu öğretici, kendi Kiracı sağlama yapmadan eylem örnek toosee kullanabileceğiniz önceden sağlanan değerlerin hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="296b0-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="296b0-152">Ancak, bu adımı gerçekleştirmek ve kendi uygulamaları oluştururken gerekli olacağı için hello işlemiyle aşina öneririz.</span><span class="sxs-lookup"><span data-stu-id="296b0-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="296b0-153">Azure AD uygulamaları bilinen belirteçleri tooonly verir.</span><span class="sxs-lookup"><span data-stu-id="296b0-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="296b0-154">Azure AD, uygulamanızdan kullanmadan önce toocreate bir girdi için kiracınızda gerekir.</span><span class="sxs-lookup"><span data-stu-id="296b0-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="296b0-155">Yeni bir uygulama kiracınızda tooregister:</span><span class="sxs-lookup"><span data-stu-id="296b0-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="296b0-156">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="296b0-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="296b0-157">Merhaba üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="296b0-157">On hello top bar, click your account.</span></span> <span data-ttu-id="296b0-158">Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="296b0-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="296b0-159">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="296b0-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="296b0-160">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="296b0-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="296b0-161">Merhaba komut istemlerini izleyin ve oluşturma bir **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="296b0-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="296b0-162">(Cordova uygulamaları HTML bağlı olsa da, bir yerel istemci uygulaması oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="296b0-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="296b0-163">Merhaba **yerel istemci uygulaması** seçeneği seçili olmalıdır veya Merhaba uygulaması çalışmayacak.)</span><span class="sxs-lookup"><span data-stu-id="296b0-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="296b0-164">**Ad** uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="296b0-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="296b0-165">**Yeniden yönlendirme URI'si** hello tooreturn belirteçleri tooyour uygulama kullanılan URI değil.</span><span class="sxs-lookup"><span data-stu-id="296b0-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="296b0-166">Girin **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="296b0-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="296b0-167">Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği tooyour uygulama atar.</span><span class="sxs-lookup"><span data-stu-id="296b0-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="296b0-168">Bu değer hello sonraki bölümlerde gerekir.</span><span class="sxs-lookup"><span data-stu-id="296b0-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="296b0-169">Merhaba uygulama sekmesinde yeni uygulama oluşturulan hello bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="296b0-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="296b0-170">toorun `DirSearchClient Sample`, yeni oluşturulan hello uygulama izni tooquery hello Azure AD Graph API verin:</span><span class="sxs-lookup"><span data-stu-id="296b0-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="296b0-171">Merhaba gelen **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="296b0-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="296b0-172">Hello Azure Active Directory uygulamasını seçmek **Microsoft Graph** olarak API hello ve hello ekleyin **erişim hello dizini hello oturum açmış kullanıcı olarak** altında izni **atanan İzinleri**.</span><span class="sxs-lookup"><span data-stu-id="296b0-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="296b0-173">Bu, kullanıcılar için uygulama tooquery hello grafik API'si sağlar.</span><span class="sxs-lookup"><span data-stu-id="296b0-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="296b0-174">2. adım: hello örnek uygulama depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="296b0-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="296b0-175">Kabuk veya komut satırı hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="296b0-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="296b0-176">3. adım: Merhaba Cordova uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="296b0-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="296b0-177">Birden çok yol toocreate Cordova uygulamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="296b0-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="296b0-178">Bu öğreticide, hello Cordova komut satırı arabirimi (CLI) kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="296b0-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="296b0-179">Kabuk veya komut satırı hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="296b0-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="296b0-180">Bu komut, hello klasör yapısını ve hello Cordova projesi için askılamayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="296b0-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="296b0-181">Toohello yeni DirSearchClient klasör taşınamadı:</span><span class="sxs-lookup"><span data-stu-id="296b0-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="296b0-182">Hello başlangıç projesi Merhaba içeriğine, Dosya Yöneticisi veya, kabuk komutu aşağıdaki hello kullanarak hello www alt klasörüne kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="296b0-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="296b0-183">Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="296b0-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="296b0-184">Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="296b0-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="296b0-185">Merhaba beyaz liste eklentisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="296b0-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="296b0-186">Bu, hello grafik API'si çağırma için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="296b0-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="296b0-187">Toosupport istediğiniz tüm hello platformlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="296b0-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="296b0-188">bir çalışma örneği toohave, tooexecute en az bir komutları aşağıdaki Merhaba, gerekir.</span><span class="sxs-lookup"><span data-stu-id="296b0-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="296b0-189">Olmaz mümkün tooemulate iOS Windows olması veya bir Mac bilgisayar Windows'ta öykünmek unutmayın</span><span class="sxs-lookup"><span data-stu-id="296b0-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="296b0-190">Cordova eklentisi tooyour projesi için ADAL Hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="296b0-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="296b0-191">4. adım: kodu tooauthenticate kullanıcı ekleyin ve Azure AD'den belirteçleri elde</span><span class="sxs-lookup"><span data-stu-id="296b0-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="296b0-192">Bu öğreticide geliştirirken Merhaba uygulaması bir Basit Dizin arama özelliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="296b0-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="296b0-193">Merhaba kullanıcı daha sonra hello dizini hello diğer herhangi bir kullanıcı adını yazın ve bazı temel öznitelikler görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="296b0-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="296b0-194">Merhaba başlangıç projesi hello tanımı hello temel kullanıcı arabiriminin hello uygulamada (www/index.html) içerir ve temel uygulama olay bağlayan hello yapı iskelesi, kullanıcı arabirimi bağlamaları döngüleri görüntü mantığında (www/js/index.js) sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="296b0-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="296b0-195">Merhaba, sol yalnızca kimlik görevleri uygulayan tooadd hello mantığı bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="296b0-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="296b0-196">Merhaba kodunuzda toodo gereken ilk şey uygulamanızı tanımlamak için Azure AD kullanır hello Protokolü değerleri tanıtmak olduğunu ve kaynakları, hedefleyen hello.</span><span class="sxs-lookup"><span data-stu-id="296b0-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="296b0-197">Bu değerleri kullanılan tooconstruct hello belirteç isteklerini daha sonra olacaktır.</span><span class="sxs-lookup"><span data-stu-id="296b0-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="296b0-198">Aşağıdaki kod parçacığında hello dosyanın üst kısmındaki hello index.js hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="296b0-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="296b0-199">Merhaba `redirectUri` ve `clientId` değerleri, uygulamanızı Azure AD'de açıklayan hello değerler eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="296b0-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="296b0-200">Merhaba olanlardan bulabilirsiniz **yapılandırma** 1. adımda Bu öğreticide daha önce açıklandığı gibi hello Azure portal sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="296b0-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="296b0-201">Yeni bir uygulama, kendi Kiracı kayıt değil için ettiyseniz, olduğu gibi hello önceden yapılandırılmış değerleri yalnızca yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="296b0-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="296b0-202">Üretim için yöneliktir uygulamalarınız için her zaman kendi giriş oluşturmalısınız olsa hello örnek çalıştıran, daha sonra görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="296b0-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="296b0-203">Ardından, hello belirteç isteği kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="296b0-203">Next, add hello token request code.</span></span> <span data-ttu-id="296b0-204">Merhaba arasında parçacığını aşağıdaki hello Ekle `search` ve `renderData` tanımları:</span><span class="sxs-lookup"><span data-stu-id="296b0-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="296b0-205">Bu işlev, iki ana bölüme çiğnemekten tarafından inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="296b0-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="296b0-206">Bu örnek karşılıklı toobeing tooa belirli bir bağlı tasarlanmış toowork tüm Kiracı ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="296b0-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="296b0-207">Merhaba kullanan hello kullanıcı tooenter herhangi bir hesabı kimlik doğrulaması anında sağlar ve ait olduğu hello isteği toohello Kiracı yönlendirir "/ ortak" uç nokta.</span><span class="sxs-lookup"><span data-stu-id="296b0-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="296b0-208">Bir belirteç zaten depolanıyorsa hello ADAL önbellek toosee hello yöntemi ilk bu parçası olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="296b0-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="296b0-209">Bu durumda, hello yöntemi nereden hello belirteci ADAL yeniden geldiğini hello kiracılar kullanır.</span><span class="sxs-lookup"><span data-stu-id="296b0-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="296b0-210">Bu gerekli tooavoid hello kullan "/ ortak", her zaman yeni bir hesap hello kullanıcı tooenter soran içinde sonuçları fazladan istemleri olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="296b0-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="296b0-211">Merhaba yöntemi Hello ikinci bölümü hello uygun belirteç isteği gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="296b0-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="296b0-212">Merhaba `acquireTokenSilentAsync` yöntemi belirtilen hello için bir belirteç ADAL tooreturn ister herhangi UX gösteren olmadan kaynak</span><span class="sxs-lookup"><span data-stu-id="296b0-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="296b0-213">Merhaba önbellek depolanan, uygun erişim belirteci zaten varsa oluşabilir veya bir yenileme belirteci olup olmadığını kullanılan tooget yeni bir erişim belirteci herhangi bir istem göstermeden.</span><span class="sxs-lookup"><span data-stu-id="296b0-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="296b0-214">O deneme başarısız olursa, biz geri dönmesi `acquireTokenAsync`--hangi görünür şekilde ister hello kullanıcı tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="296b0-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="296b0-215">Biz hello belirteci sahip olduğunuza göre biz son hello grafik API'si çağırma ve istiyoruz hello arama sorgusu gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="296b0-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="296b0-216">Merhaba aşağıdaki kod parçacığını aşağıdaki hello Ekle `authenticate` tanımı:</span><span class="sxs-lookup"><span data-stu-id="296b0-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="296b0-217">bir kullanıcının diğer adı metin kutusuna girmek için basit bir UX sağladığı Hello başlangıç noktası dosyalar.</span><span class="sxs-lookup"><span data-stu-id="296b0-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="296b0-218">Bu yöntem tooconstruct bir sorgu değeri, hello erişim belirteciyle birleştirmek, tooMicrosoft grafik göndermek ve hello sonuçlarını ayrıştırmak kullanır.</span><span class="sxs-lookup"><span data-stu-id="296b0-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="296b0-219">Merhaba `renderData` yöntemi, hello başlangıç noktası dosyasında zaten mevcut hello sonuçlarını görselleştirme mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="296b0-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="296b0-220">Adım 5: hello uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="296b0-220">Step 5: Run hello app</span></span>
<span data-ttu-id="296b0-221">Uygulamanız son hazır toorun ' dir.</span><span class="sxs-lookup"><span data-stu-id="296b0-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="296b0-222">Bu işletim basittir: hello uygulama başlatıldığında hello diğer yukarı toolook istediğiniz hello kullanıcı adını girin ve sonra hello düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="296b0-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="296b0-223">Kimlik doğrulaması için istenir.</span><span class="sxs-lookup"><span data-stu-id="296b0-223">You're prompted for authentication.</span></span> <span data-ttu-id="296b0-224">Başarılı kimlik doğrulama ve başarılı arama sırasında aranır hello kullanıcı hello özniteliklerini görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="296b0-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="296b0-225">Sonraki çalıştırır, herhangi bir istem göstermeden hello arama gerçekleştirilir, thanks hello toohello varlığını önceden önbelleğinde belirteç alındı.</span><span class="sxs-lookup"><span data-stu-id="296b0-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="296b0-226">Merhaba uygulama çalıştırmaya hello somut adımları platforma göre değişir.</span><span class="sxs-lookup"><span data-stu-id="296b0-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="296b0-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="296b0-227">Windows 10</span></span>
   <span data-ttu-id="296b0-228">Tablet/bilgisayar:`cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="296b0-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="296b0-229">Mobil (Windows 10 Mobile cihaz bağlı tooa PC gerektirir):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="296b0-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="296b0-230">İlk çalıştırma hello sırasında içinde toosign Geliştirici lisansı istenebilir.</span><span class="sxs-lookup"><span data-stu-id="296b0-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="296b0-231">Daha fazla bilgi için bkz: [Geliştirici lisansı](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="296b0-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="296b0-232">Windows 8.1 Tablet/PC</span><span class="sxs-lookup"><span data-stu-id="296b0-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="296b0-233">İlk çalıştırma hello sırasında içinde toosign Geliştirici lisansı istenebilir.</span><span class="sxs-lookup"><span data-stu-id="296b0-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="296b0-234">Daha fazla bilgi için bkz: [Geliştirici lisansı](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="296b0-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="296b0-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="296b0-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="296b0-236">bağlı bir cihazda toorun:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="296b0-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="296b0-237">toorun hello varsayılan öykünücü üzerinde:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="296b0-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="296b0-238">Kullanım `cordova run windows --list -- --phone` toosee tüm kullanılabilir hedefler ve `cordova run windows --target=<target_name> -- --phone` toorun Merhaba uygulaması belirli cihaz veya öykünücü (örneğin, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="296b0-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="296b0-239">Android</span><span class="sxs-lookup"><span data-stu-id="296b0-239">Android</span></span>
   <span data-ttu-id="296b0-240">bağlı bir cihazda toorun:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="296b0-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="296b0-241">toorun hello varsayılan öykünücü üzerinde:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="296b0-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="296b0-242">Bir öykünücü örneğinde AVD Yöneticisi'ni kullanarak daha önce hello "Önkoşullar" bölümünde açıklandığı gibi oluşturduğunuz emin olun.</span><span class="sxs-lookup"><span data-stu-id="296b0-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="296b0-243">Kullanım `cordova run android --list` toosee tüm kullanılabilir hedefler ve `cordova run android --target=<target_name>` toorun Merhaba uygulaması belirli cihaz veya öykünücü (örneğin, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="296b0-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="296b0-244">iOS</span><span class="sxs-lookup"><span data-stu-id="296b0-244">iOS</span></span>
   <span data-ttu-id="296b0-245">bağlı bir cihazda toorun:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="296b0-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="296b0-246">toorun hello varsayılan öykünücü üzerinde:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="296b0-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="296b0-247">Merhaba olduğundan emin olun `ios-sim` hello öykünücüsü üzerinde yüklü paket toorun.</span><span class="sxs-lookup"><span data-stu-id="296b0-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="296b0-248">Daha fazla bilgi için bkz: hello "Önkoşullar" bölümü.</span><span class="sxs-lookup"><span data-stu-id="296b0-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="296b0-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="296b0-249">Next steps</span></span>
<span data-ttu-id="296b0-250">Başvuru için (yapılandırma değerleriniz olmadan) tamamlandı hello örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="296b0-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="296b0-251">Şimdi Gelişmiş toomore (ve daha ilginç) taşıma senaryoları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="296b0-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="296b0-252">Tootry isteyebilirsiniz: [Azure AD ile bir Node.js Web API'SİNİN güvenliğini](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="296b0-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
