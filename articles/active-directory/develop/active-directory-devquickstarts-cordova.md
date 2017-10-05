---
title: "Azure AD Cordova Başlarken | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleştirilen ve OAuth kullanarak Azure AD korumalı API çağıran bir Cordova uygulaması oluşturma."
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
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="34e85-103">Azure AD tümleştirme bir Apache Cordova uygulaması</span><span class="sxs-lookup"><span data-stu-id="34e85-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="34e85-104">Apache Cordova mobil aygıtlarda tam özellikli yerel uygulamalar olarak çalıştırabilirsiniz HTML5/JavaScript uygulamaları geliştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="34e85-105">Azure Active Directory ile (Azure AD), Cordova uygulamalarınızı Kurumsal düzeyde kimlik doğrulama özellikleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="34e85-106">Cordova eklentisi Azure sarmalar AD yerel SDK'ları iOS, Android, Windows mağazası ve Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="34e85-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="34e85-107">Kullanarak eklenti, oturum açma, kullanıcılarınızın Windows Server Active Directory hesaplarıyla desteklemek, Office 365 ve Azure API'lerini erişmek ve hatta kendi özel web API çağrıları korunmasına yardımcı olmak için uygulamanızın geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="34e85-108">Bu öğreticide, aşağıdaki özellikler ekleyerek basit bir uygulama geliştirmek için Active Directory Authentication Library (ADAL) için eklenti Apache Cordova kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="34e85-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="34e85-109">Yalnızca birkaç satır kod ile bir kullanıcının kimliğini doğrulamak ve bir belirteç elde edin.</span><span class="sxs-lookup"><span data-stu-id="34e85-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="34e85-110">Bu dizini sorgulayabilir ve sonuçları görüntülemek için grafik API'sini çağırmak için bu belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="34e85-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="34e85-111">Kullanıcı için kimlik doğrulaması ister en aza indirmek için ADAL belirteç önbelleği kullanın.</span><span class="sxs-lookup"><span data-stu-id="34e85-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="34e85-112">Bu geliştirmeler yapmak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="34e85-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="34e85-113">Bir uygulamayı Azure AD'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34e85-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="34e85-114">Belirteç isteme uygulamanıza kod ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34e85-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="34e85-115">Grafik API'si sorgulamak için belirteci kullanın için kodu ekleyin ve sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="34e85-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="34e85-116">Hedef, Cordova ADAL eklenti eklemek ve Öykünücüler çözümü test istediğiniz tüm platformlar ile Cordova dağıtım projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="34e85-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34e85-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="34e85-117">Prerequisites</span></span>
<span data-ttu-id="34e85-118">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="34e85-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="34e85-119">Uygulama geliştirme hakları olan bir hesabın sahip olduğu bir Azure AD kiracısı.</span><span class="sxs-lookup"><span data-stu-id="34e85-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="34e85-120">Apache Cordova kullanmak üzere yapılandırılmış bir geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="34e85-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="34e85-121">Her ikisi de varsa, ayarlamak, doğrudan adım 1 geçin.</span><span class="sxs-lookup"><span data-stu-id="34e85-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="34e85-122">Azure AD kiracısı yoksa kullanmak [nasıl edinebileceğinizi yönergeler](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="34e85-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="34e85-123">Apache Cordova makinenizde ayarlanan yoksa, aşağıdaki yükleyin:</span><span class="sxs-lookup"><span data-stu-id="34e85-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="34e85-124">Git</span><span class="sxs-lookup"><span data-stu-id="34e85-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="34e85-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="34e85-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="34e85-126">[Cordova CLI](https://cordova.apache.org/) (NPM Paket Yöneticisi kolayca yüklenebilir: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="34e85-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="34e85-127">Önceki yüklemeleri PC ve Mac çalışması gerekir</span><span class="sxs-lookup"><span data-stu-id="34e85-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="34e85-128">Her hedef platformu farklı Önkoşullar vardır:</span><span class="sxs-lookup"><span data-stu-id="34e85-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="34e85-129">Derleme ve Windows Tablet/PC veya Windows Phone için bir uygulamayı çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="34e85-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="34e85-130">Yükleme [Windows Update 2 veya sonraki sürümü için Visual Studio 2013](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express veya başka bir sürümü) veya [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="34e85-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="34e85-131">Derleme ve iOS için uygulama çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="34e85-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="34e85-132">Xcode yükleme 6.x veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="34e85-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="34e85-133">İndirin [Apple Developer site](http://developer.apple.com/downloads) veya [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="34e85-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="34e85-134">Yükleme [ios-SIM](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="34e85-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="34e85-135">İOS uygulamaları iOS simülatörü komut satırından başlatmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="34e85-136">(Kolayca terminal yükleyebilirsiniz: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="34e85-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="34e85-137">Derleme ve Android için uygulama çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="34e85-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="34e85-138">Yükleme [Java Geliştirme Seti (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="34e85-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="34e85-139">Emin olun `JAVA_HOME` (ortam değişkeni) JDK yükleme yolu (örneğin, C:\Program Files\Java\jdk1.7.0_75) göre doğru olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="34e85-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="34e85-140">Yükleme [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) ve ekleme `<android-sdk-location>\tools` konuma (örneğin, C:\tools\Android\android-sdk\tools), `PATH` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="34e85-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="34e85-141">Android SDK Yöneticisi'ni açın (örneğin, terminal aracılığıyla: `android`) ve yükleyin:</span><span class="sxs-lookup"><span data-stu-id="34e85-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="34e85-142">*Android 5.0.1 (API 21)* platform SDK'si</span><span class="sxs-lookup"><span data-stu-id="34e85-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="34e85-143">*Android SDK derleme araçlarını* sürüm 19.1.0 veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="34e85-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="34e85-144">*Android desteği depo* (ek özellikler)</span><span class="sxs-lookup"><span data-stu-id="34e85-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="34e85-145">Android SDK varsayılan öykünücü örnek sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="34e85-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="34e85-146">Çalıştırarak oluşturmak `android avd` terminalde seçilerek **oluşturma**, Android uygulaması bir öykünücüsünde çalıştırmak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="34e85-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="34e85-147">19 veya daha yüksek bir API düzeyi öneririz.</span><span class="sxs-lookup"><span data-stu-id="34e85-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="34e85-148">Android öykünücü ve oluşturma seçenekleri hakkında daha fazla bilgi için bkz: [AVD Yöneticisi](http://developer.android.com/tools/help/avd-manager.html) Android sitesinde.</span><span class="sxs-lookup"><span data-stu-id="34e85-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="34e85-149">1. adım: bir uygulamayı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="34e85-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="34e85-150">Bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34e85-150">This step is optional.</span></span> <span data-ttu-id="34e85-151">Bu öğretici, kendi Kiracı sağlama yapmadan eylem örnek görmek için kullanabileceğiniz önceden sağlanan değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="34e85-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="34e85-152">Ancak, bu adımı gerçekleştirmek ve kendi uygulamaları oluştururken gerekli olacağı için işlemiyle aşina öneririz.</span><span class="sxs-lookup"><span data-stu-id="34e85-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="34e85-153">Azure AD yalnızca bilinen uygulamalara belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="34e85-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="34e85-154">Azure AD, uygulamanızdan kullanabilmeniz için önce bir girdi için kiracınızda oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="34e85-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="34e85-155">Yeni bir uygulama kiracınızda kaydetmek için:</span><span class="sxs-lookup"><span data-stu-id="34e85-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="34e85-156">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="34e85-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="34e85-157">Üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="34e85-157">On the top bar, click your account.</span></span> <span data-ttu-id="34e85-158">İçinde **Directory** listesinde, Azure AD Kiracı uygulamanızı kaydetmek istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="34e85-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="34e85-159">Tıklatın **daha Hizmetleri** sol bölmesinde ve seçip **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="34e85-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="34e85-160">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="34e85-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="34e85-161">Komut istemlerini izleyin ve oluşturun bir **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="34e85-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="34e85-162">(Cordova uygulamaları HTML bağlı olsa da, bir yerel istemci uygulaması oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="34e85-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="34e85-163">**Yerel istemci uygulaması** seçeneği seçili olmalıdır veya uygulama çalışmaz.)</span><span class="sxs-lookup"><span data-stu-id="34e85-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="34e85-164">**Ad** kullanıcılar uygulamanıza açıklar.</span><span class="sxs-lookup"><span data-stu-id="34e85-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="34e85-165">**Yeniden yönlendirme URI'si** belirteçleri uygulamanıza döndürmek için kullanılan bir URI.</span><span class="sxs-lookup"><span data-stu-id="34e85-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="34e85-166">Girin **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="34e85-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="34e85-167">Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği uygulamanıza atar.</span><span class="sxs-lookup"><span data-stu-id="34e85-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="34e85-168">Bu değeri sonraki bölümlerde bulunan gerekir.</span><span class="sxs-lookup"><span data-stu-id="34e85-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="34e85-169">Yeni oluşturulan uygulama uygulama sekmesinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="34e85-170">Çalıştırmak için `DirSearchClient Sample`, Azure AD Graph API sorgulamak için yeni oluşturulan uygulama izni verin:</span><span class="sxs-lookup"><span data-stu-id="34e85-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="34e85-171">Gelen **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="34e85-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="34e85-172">Azure Active Directory uygulaması için seçin **Microsoft Graph** API olarak ve ekleme **gibi oturum açan kullanıcının dizine erişim** altında izni **izinlere temsilci**.</span><span class="sxs-lookup"><span data-stu-id="34e85-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="34e85-173">Bu kullanıcılar için grafik API'si sorgulamak uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="34e85-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="34e85-174">2. adım: örnek uygulama depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="34e85-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="34e85-175">Kabuk veya komut satırı, aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="34e85-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="34e85-176">3. adım: Cordova uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="34e85-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="34e85-177">Cordova uygulamaları oluşturmak için birden çok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="34e85-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="34e85-178">Bu öğreticide, Cordova komut satırı arabirimi (CLI) kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="34e85-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="34e85-179">Kabuk veya komut satırı, aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="34e85-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="34e85-180">Bu komut, Cordova projesi için askılamayı ve klasör yapısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="34e85-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="34e85-181">Yeni DirSearchClient klasöre gidin:</span><span class="sxs-lookup"><span data-stu-id="34e85-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="34e85-182">Başlangıç projesi içeriğini Kabuğu'nda Dosya Yöneticisi veya aşağıdaki komutu kullanarak www alt klasöründe kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="34e85-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="34e85-183">Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="34e85-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="34e85-184">Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="34e85-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="34e85-185">Beyaz liste eklentisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34e85-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="34e85-186">Bu grafik API'sini çağırma için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="34e85-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="34e85-187">Desteklemek istediğiniz tüm platformlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34e85-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="34e85-188">Bir çalışma örneği için en az biri aşağıdaki komutları yürütün gerekir.</span><span class="sxs-lookup"><span data-stu-id="34e85-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="34e85-189">Windows İos'ta öykünmek veya bir Mac bilgisayar Windows'ta öykünmek mümkün olmayacaktır unutmayın</span><span class="sxs-lookup"><span data-stu-id="34e85-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="34e85-190">ADAL Cordova eklentisi projenize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="34e85-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="34e85-191">4. adım: kullanıcıların kimlik doğrulaması ve Azure AD'den belirteçleri elde etmek için kod ekleme</span><span class="sxs-lookup"><span data-stu-id="34e85-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="34e85-192">Bu öğreticide geliştirirken uygulama bir Basit Dizin arama özelliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="34e85-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="34e85-193">Kullanıcı dizindeki diğer herhangi bir kullanıcı adını yazın ve bazı temel öznitelikler görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="34e85-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="34e85-194">Başlangıç projesi uygulamada (www/index.html) temel kullanıcı arabiriminin tanımını içerir ve temel uygulama olay bağlayan yapı iskelesi, kullanıcı arabirimi bağlamaları geçiş yapar ve görüntü mantığında (www/js/index.js) sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="34e85-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="34e85-195">Sizin için sol yalnızca kimlik görevleri uygulayan mantığı eklemek için bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="34e85-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="34e85-196">Kodunuzda yapmanız gereken ilk şey, Azure AD uygulamanızı ve kaynakları tanımlamak için kullandığı Protokolü değerleri, hedefleyen tanıtmak ' dir.</span><span class="sxs-lookup"><span data-stu-id="34e85-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="34e85-197">Bu değerler, belirteç isteklerini daha sonra oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34e85-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="34e85-198">Aşağıdaki kod parçacığında index.js dosyanın üst kısmında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="34e85-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="34e85-199">`redirectUri` Ve `clientId` değerleri, uygulamanızı Azure AD'de açıklayan değerler eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="34e85-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="34e85-200">Olanlardan bulabilirsiniz **yapılandırma** 1. adımda Bu öğreticide daha önce açıklandığı gibi Azure portalında sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="34e85-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="34e85-201">Yeni bir uygulama, kendi Kiracı kayıt değil için ettiyseniz, olduğu gibi önceden yapılandırılmış değerleri yalnızca yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="34e85-202">Üretim için yöneliktir uygulamalarınız için her zaman kendi giriş oluşturmalısınız rağmen çalışan, örnek görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="34e85-203">Ardından, belirteci isteği kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34e85-203">Next, add the token request code.</span></span> <span data-ttu-id="34e85-204">Aşağıdaki kod parçacığını arasında Ekle `search` ve `renderData` tanımları:</span><span class="sxs-lookup"><span data-stu-id="34e85-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="34e85-205">Bu işlev, iki ana bölüme çiğnemekten tarafından inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="34e85-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="34e85-206">Bu örnek, belirli bir bağlı tüm Kiracı çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34e85-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="34e85-207">Kullanıcının kimlik doğrulaması anında herhangi bir hesabı girmesini sağlar ve Kiracı isteğine ait olduğu yönlendirir "/ ortak" endpoint kullanır.</span><span class="sxs-lookup"><span data-stu-id="34e85-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="34e85-208">Bu yöntem ilk kısmı bir belirteç zaten depolanmış görmek için ADAL önbelleğin olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="34e85-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="34e85-209">Öyleyse, yöntem nereden belirteç ADAL yeniden geldiğini kiracılar kullanır.</span><span class="sxs-lookup"><span data-stu-id="34e85-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="34e85-210">"/ Ortak", kullanım her zaman yeni bir hesabı girmesini isteyen sonuçlandığından bu fazladan istemleri önlemek gereklidir.</span><span class="sxs-lookup"><span data-stu-id="34e85-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="34e85-211">Yöntemin ikinci bölümü doğru belirteci isteği gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="34e85-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="34e85-212">`acquireTokenSilentAsync` Yöntemi, belirtilen kaynak için bir belirteç herhangi UX göstermeden dönmek için ADAL sorar</span><span class="sxs-lookup"><span data-stu-id="34e85-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="34e85-213">Önbellekte depolanan, uygun erişim belirteci zaten varsa oluşabilir veya bir yenileme belirteci herhangi bir istem göstermeden yeni bir erişim belirteci almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="34e85-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="34e85-214">O deneme başarısız olursa, biz geri dönmesi `acquireTokenAsync`--hangi görünür şekilde ister kullanıcının kimlik doğrulamasını.</span><span class="sxs-lookup"><span data-stu-id="34e85-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="34e85-215">Biz belirtece sahip olduğunuza göre biz son grafik API'sini çağırmak ve istiyoruz arama sorgusu gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="34e85-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="34e85-216">Aşağıdaki kod parçacığını aşağıdaki Ekle `authenticate` tanımı:</span><span class="sxs-lookup"><span data-stu-id="34e85-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
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
<span data-ttu-id="34e85-217">Başlangıç noktası dosyaları, metin kutusuna bir kullanıcının diğer adı girmek için basit bir UX sağlanan.</span><span class="sxs-lookup"><span data-stu-id="34e85-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="34e85-218">Bu yöntem, bir sorgu oluşturun, erişim belirteciyle birleştirmek, Microsoft Graph göndermek ve sonuçlarını ayrıştırmak için bu değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="34e85-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="34e85-219">`renderData` Yöntemi, başlangıç noktası dosyasında zaten mevcut sonuçlarını görselleştirme mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="34e85-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="34e85-220">5. adım: uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="34e85-220">Step 5: Run the app</span></span>
<span data-ttu-id="34e85-221">Uygulamanızı çalıştırmak son hazırdır.</span><span class="sxs-lookup"><span data-stu-id="34e85-221">Your app is finally ready to run.</span></span> <span data-ttu-id="34e85-222">Bu işletim basittir: uygulama başlatıldığında diğer aramak istediğiniz kullanıcının adını girin ve ardından düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34e85-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="34e85-223">Kimlik doğrulaması için istenir.</span><span class="sxs-lookup"><span data-stu-id="34e85-223">You're prompted for authentication.</span></span> <span data-ttu-id="34e85-224">Başarılı kimlik doğrulama ve başarılı arama sırasında aranan kullanıcı özniteliklerini görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="34e85-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="34e85-225">Sonraki çalıştırır, önceden alınmış belirtecin önbelleğinde varlığını sayesinde hiçbir istemi göstermeden arama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="34e85-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="34e85-226">Uygulamayı çalıştırmak için somut adımları platforma göre değişir.</span><span class="sxs-lookup"><span data-stu-id="34e85-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="34e85-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="34e85-227">Windows 10</span></span>
   <span data-ttu-id="34e85-228">Tablet/bilgisayar:`cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="34e85-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="34e85-229">Mobil (bir Bilgisayara bağlı bir Windows 10 mobil aygıt gerektirir):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="34e85-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="34e85-230">İlk çalıştırmada Geliştirici lisansı oturum açmak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="34e85-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="34e85-231">Daha fazla bilgi için bkz: [Geliştirici lisansı](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="34e85-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="34e85-232">Windows 8.1 Tablet/PC</span><span class="sxs-lookup"><span data-stu-id="34e85-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="34e85-233">İlk çalıştırmada Geliştirici lisansı oturum açmak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="34e85-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="34e85-234">Daha fazla bilgi için bkz: [Geliştirici lisansı](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="34e85-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="34e85-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="34e85-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="34e85-236">Bağlı bir cihaza çalıştırmak için:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="34e85-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="34e85-237">Varsayılan öykünücüsünde çalıştırmak için:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="34e85-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="34e85-238">Kullanım `cordova run windows --list -- --phone` tüm kullanılabilir hedefleri görmek için ve `cordova run windows --target=<target_name> -- --phone` belirli cihaz veya öykünücü üzerinde uygulamayı çalıştırmak için (örneğin, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="34e85-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="34e85-239">Android</span><span class="sxs-lookup"><span data-stu-id="34e85-239">Android</span></span>
   <span data-ttu-id="34e85-240">Bağlı bir cihaza çalıştırmak için:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="34e85-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="34e85-241">Varsayılan öykünücüsünde çalıştırmak için:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="34e85-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="34e85-242">Bir öykünücü örneğinde AVD Yöneticisi'ni kullanarak daha önce "Önkoşullar" bölümünde açıklandığı gibi oluşturduğunuz emin olun.</span><span class="sxs-lookup"><span data-stu-id="34e85-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="34e85-243">Kullanım `cordova run android --list` tüm kullanılabilir hedefleri görmek için ve `cordova run android --target=<target_name>` belirli cihaz veya öykünücü üzerinde uygulamayı çalıştırmak için (örneğin, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="34e85-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="34e85-244">iOS</span><span class="sxs-lookup"><span data-stu-id="34e85-244">iOS</span></span>
   <span data-ttu-id="34e85-245">Bağlı bir cihaza çalıştırmak için:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="34e85-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="34e85-246">Varsayılan öykünücüsünde çalıştırmak için:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="34e85-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="34e85-247">Olduğundan emin olun `ios-sim` öykünücüsünde çalıştırmak için yüklü paket.</span><span class="sxs-lookup"><span data-stu-id="34e85-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="34e85-248">Daha fazla bilgi için "Önkoşullar" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="34e85-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="34e85-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34e85-249">Next steps</span></span>
<span data-ttu-id="34e85-250">Başvuru için (yapılandırma değerleriniz olmadan) tamamlanan örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="34e85-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="34e85-251">Artık daha gelişmiş (ve daha ilginç) senaryolara geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e85-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="34e85-252">Denemek isteyebilirsiniz: [Azure AD ile bir Node.js Web API'SİNİN güvenliğini](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="34e85-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
