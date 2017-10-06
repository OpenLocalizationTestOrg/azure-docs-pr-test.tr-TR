---
title: "aaaAzure AD Başlarken Android | Microsoft Docs"
description: "Nasıl toobuild oturum açma ve Azure AD aramalar için Azure AD ile tümleşen bir Android uygulaması API'leri OAuth kullanılarak korunan."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="00b15-103">Android uygulamaya Azure AD tümleştirme</span><span class="sxs-lookup"><span data-stu-id="00b15-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="00b15-104">Bizim yeni Hello önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/Android), hangi yardımcı olacak birkaç dakika içinde Azure AD ile başlamak ve çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="00b15-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="00b15-105">Merhaba Geliştirici Portalı, bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme hello işleminde size rehberlik yapar.</span><span class="sxs-lookup"><span data-stu-id="00b15-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="00b15-106">İşiniz bittiğinde, bu belirteçleri kabul edebilir ve doğrulama gerçekleştirmek kullanıcılar, Kiracı ve arka uç kimlik doğrulaması yapabilir basit bir uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="00b15-107">Bir masaüstü uygulaması geliştiriyorsanız, Azure Active Directory (Azure AD), basit ve kolay, tooauthenticate için kullanıcılarınız, şirket içi Active Directory hesaplarını kullanarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="00b15-108">Ayrıca, uygulama toosecurely sağlar Office 365 API'leri hello veya Azure API hello gibi tüm web Azure AD tarafından korunan API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="00b15-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="00b15-109">Korumalı tooaccess kaynakları gereken Android istemciler için Azure AD hello Active Directory Authentication Library (ADAL) sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="00b15-110">ADAL tek amacı Hello toomake Bu, uygulama tooget erişim belirteçleri için kolay.</span><span class="sxs-lookup"><span data-stu-id="00b15-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="00b15-111">toodemonstrate ne kadar kolay olduğu, biz Android Yapılacaklar listesi uygulaması, yapı:</span><span class="sxs-lookup"><span data-stu-id="00b15-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="00b15-112">Alır erişim belirteçleri hello kullanarak bir Yapılacaklar listesi API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="00b15-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="00b15-113">Bir kullanıcının yapılacaklar listesini alır.</span><span class="sxs-lookup"><span data-stu-id="00b15-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="00b15-114">Oturumunu kullanıcılar kapatır.</span><span class="sxs-lookup"><span data-stu-id="00b15-114">Signs out users.</span></span>

<span data-ttu-id="00b15-115">başlatılan tooget, kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="00b15-116">Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="00b15-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="00b15-117">1. adım: İndirme ve hello Node.js REST API TODO örnek sunucusu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="00b15-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="00b15-118">Merhaba Node.js REST API Yapılacaklar örnek özellikle toowork tek-Kiracı Yapılacaklar REST API'si için Azure AD oluşturmak için varolan örneğimizde karşı yazılır.</span><span class="sxs-lookup"><span data-stu-id="00b15-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="00b15-119">Bu hello Hızlı Başlangıç için bir önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="00b15-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="00b15-120">Nasıl tooset Bu, bkz: Varolan örneklerimizi hakkında bilgi için [Microsoft Azure Active Directory örnek REST API'si hizmeti için Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="00b15-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="00b15-121">2. adım: Azure AD kiracınıza ile web API kaydetme</span><span class="sxs-lookup"><span data-stu-id="00b15-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="00b15-122">Active Directory, iki tür uygulamaları ekleme destekler:</span><span class="sxs-lookup"><span data-stu-id="00b15-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="00b15-123">Web Hizmetleri toousers teklif API'leri</span><span class="sxs-lookup"><span data-stu-id="00b15-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="00b15-124">Web API'leri olanlar erişim (Merhaba Web'de veya bir aygıtta çalışan) uygulamaları</span><span class="sxs-lookup"><span data-stu-id="00b15-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="00b15-125">Bu adımda, bu örnek test etmek için yerel olarak çalıştırıyorsanız hello web API kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="00b15-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="00b15-126">Normalde, bu web API uygulama tooaccess istediğiniz teklifi işlevselliği bir REST hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="00b15-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="00b15-127">Azure AD, herhangi bir uç nokta korumaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="00b15-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="00b15-128">Merhaba Yapılacaklar REST API daha önce başvurulan kaydetme varsayılarak.</span><span class="sxs-lookup"><span data-stu-id="00b15-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="00b15-129">Ancak bu Azure Active Directory toohelp korumak istediğiniz tüm web API çalışır.</span><span class="sxs-lookup"><span data-stu-id="00b15-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="00b15-130">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00b15-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="00b15-131">Merhaba üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="00b15-131">On hello top bar, click your account.</span></span> <span data-ttu-id="00b15-132">Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="00b15-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="00b15-133">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00b15-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="00b15-134">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="00b15-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="00b15-135">Merhaba uygulama için kolay bir ad girin (örneğin, **TodoListService**), select **Web uygulaması ve/veya Web API**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="00b15-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="00b15-136">Merhaba oturum açma URL'sini hello örnek için hello temel URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="00b15-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="00b15-137">Varsayılan olarak `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="00b15-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="00b15-138">Tıklatın **Tamam** toocomplete hello kayıt.</span><span class="sxs-lookup"><span data-stu-id="00b15-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="00b15-139">Hello sırasında Azure portal, yine de tooyour uygulama sayfasına gidin, hello uygulama kimliği değerini bulmak ve kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="00b15-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="00b15-140">Bu daha sonra uygulamanızın yapılandırırken ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="00b15-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="00b15-141">Merhaba gelen **ayarları** -> **özellikleri** sayfasında, hello uygulama kimliği URI'SİNİN güncelleştirmesi - girin `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="00b15-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="00b15-142">Değiştir `<your_tenant_name>` Azure AD kiracınıza hello adı.</span><span class="sxs-lookup"><span data-stu-id="00b15-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="00b15-143">3. adım: hello örnek Android yerel istemci uygulaması kaydetme</span><span class="sxs-lookup"><span data-stu-id="00b15-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="00b15-144">Bu örnekte, web uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-144">You must register your web application in this sample.</span></span> <span data-ttu-id="00b15-145">Bu, uygulama toocommunicate hello henüz kayıtlı web API ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="00b15-146">Azure AD Reddet tooeven, kayıtlı olduğu sürece, uygulama tooask oturum açma için izin verin.</span><span class="sxs-lookup"><span data-stu-id="00b15-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="00b15-147">Merhaba güvenlik hello modelinin parçası olan.</span><span class="sxs-lookup"><span data-stu-id="00b15-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="00b15-148">Daha önce başvurulan hello örnek uygulaması kaydettirilirken varsayılarak.</span><span class="sxs-lookup"><span data-stu-id="00b15-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="00b15-149">Ancak bu yordam, geliştirmekte herhangi bir uygulama için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="00b15-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="00b15-150">Neden, hem uygulama hem de web API'si bir kiracı koyma merak ediyor.</span><span class="sxs-lookup"><span data-stu-id="00b15-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="00b15-151">Tahmin gibi başka bir kiracı Azure AD'den kayıtlı bir API'nin erişen bir uygulama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="00b15-152">Bunu yaparsanız, müşterilerinizin olacaktır tooconsent toohello hello API hello uygulama kullanımını istenir.</span><span class="sxs-lookup"><span data-stu-id="00b15-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="00b15-153">İOS için Active Directory Authentication Library sizin için bu onay ilgilenir.</span><span class="sxs-lookup"><span data-stu-id="00b15-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="00b15-154">Biz daha gelişmiş özellikleri keşfetmenizde bu hello iş gerekli tooaccess hello paketinin Microsoft Azure ve Office yanı sıra, başka bir hizmet sağlayıcısı APIs önemli bir parçası olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="00b15-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="00b15-155">Web API ve hello uygulamanızı kayıtlı için şu an için aynı Kiracı, sizden izin göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="00b15-156">Yalnızca kendi şirket toouse için uygulama geliştirme yapıyorsanız bu genellikle hello durumdur.</span><span class="sxs-lookup"><span data-stu-id="00b15-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="00b15-157">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00b15-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="00b15-158">Merhaba üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="00b15-158">On hello top bar, click your account.</span></span> <span data-ttu-id="00b15-159">Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="00b15-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="00b15-160">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00b15-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="00b15-161">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="00b15-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="00b15-162">Merhaba uygulama için kolay bir ad girin (örneğin, **TodoListClient Android**), select **yerel istemci uygulaması**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="00b15-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="00b15-163">Merhaba yeniden yönlendirme URI'si, girin `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="00b15-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="00b15-164">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="00b15-164">Click **Finish**.</span></span>
7. <span data-ttu-id="00b15-165">Merhaba uygulama sayfasından hello uygulama kimliği değerini bulmak ve kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="00b15-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="00b15-166">Bu daha sonra uygulamanızın yapılandırırken ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="00b15-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="00b15-167">Merhaba gelen **ayarları** sayfasında, **gerekli izinler** seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="00b15-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="00b15-168">Bulun ve TodoListService seçin, hello eklemeniz **erişim TodoListService** altında izni **izinlere temsilci**, tıklatıp **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="00b15-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="00b15-169">toobuild Maven ile Merhaba en üst düzeyde pom.xml kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00b15-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="00b15-170">Bu depodaki tercih ettiğiniz bir dizine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="00b15-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="00b15-171">Merhaba Hello adımları [Önkoşullar tooset Android için Maven ortamınızı](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="00b15-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="00b15-172">Merhaba öykünücü SDK 19 ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="00b15-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="00b15-173">Merhaba depodaki kopyaladığınız toohello kök klasörden gidin.</span><span class="sxs-lookup"><span data-stu-id="00b15-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="00b15-174">Bu komutu çalıştırın:`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="00b15-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="00b15-175">Merhaba dizin toohello hızlı başlangıç örnek değiştirin:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="00b15-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="00b15-176">Bu komutu çalıştırın:`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="00b15-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="00b15-177">Merhaba uygulama başlatma görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="00b15-178">Test kullanıcı kimlik bilgilerini tootry girin.</span><span class="sxs-lookup"><span data-stu-id="00b15-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="00b15-179">JAR paketleri hello AAR paketi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="00b15-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="00b15-180">4. adım: hello Android ADAL indirin ve tooyour Eclipse çalışma Ekle</span><span class="sxs-lookup"><span data-stu-id="00b15-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="00b15-181">Bu, toohave daha kolay birden çok seçenekleri toouse ADAL Android projenize yaptık:</span><span class="sxs-lookup"><span data-stu-id="00b15-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="00b15-182">Bu kitaplığı Eclipse ve bağlantı tooyour uygulamasına hello kaynak kodu tooimport kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="00b15-183">Android Studio kullanıyorsanız, hello AAR paket biçimi ve başvuru hello ikili dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="00b15-184">Seçenek 1: Kaynak Zip</span><span class="sxs-lookup"><span data-stu-id="00b15-184">Option 1: Source Zip</span></span>
<span data-ttu-id="00b15-185">toodownload hello kaynak kodu, bir kopyasını tıklatın **ZIP'i indir** hello hello sayfasının sağ tarafında.</span><span class="sxs-lookup"><span data-stu-id="00b15-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="00b15-186">Veya [karşıdan Github'dan](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="00b15-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="00b15-187">Seçenek 2: Kaynak Git aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="00b15-187">Option 2: Source via Git</span></span>
<span data-ttu-id="00b15-188">Merhaba tooget hello kaynak kodunun Git, üzerinden yazın:</span><span class="sxs-lookup"><span data-stu-id="00b15-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="00b15-189">Seçenek 3: İkili dosyaları Gradle aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="00b15-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="00b15-190">Merhaba Maven merkezi deposu hello ikili dosyaları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="00b15-191">Android Studio projenizde Hello AAR paketi gibi eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="00b15-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="00b15-192">Seçenek 4: AAR Maven üzerinden</span><span class="sxs-lookup"><span data-stu-id="00b15-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="00b15-193">Merhaba M2Eclipse eklenti kullanıyorsanız, pom.xml dosyanızda hello bağımlılık belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00b15-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="00b15-194">5. seçenek: JAR hello libs klasörüne paketin</span><span class="sxs-lookup"><span data-stu-id="00b15-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="00b15-195">Merhaba Maven depodaki hello JAR dosyasını alın ve hello bırakma **kitaplıklar** projenizdeki klasöre.</span><span class="sxs-lookup"><span data-stu-id="00b15-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="00b15-196">Merhaba JAR paketleri dahil olmayan için toocopy hello gerekli kaynakları tooyour proje de gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="00b15-197">5. adım: başvuruları tooAndroid ADAL tooyour proje ekleme</span><span class="sxs-lookup"><span data-stu-id="00b15-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="00b15-198">Bir başvuru tooyour proje ekleyin ve bir Android kitaplığıdır belirtin.</span><span class="sxs-lookup"><span data-stu-id="00b15-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="00b15-199">Belirsiz varsa nasıl toodo bunu hello hakkında daha fazla bilgi alabileceğiniz [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="00b15-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="00b15-200">Proje ayarlarınızı hata ayıklama için hello proje bağımlılığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="00b15-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="00b15-201">Projenizin AndroidManifest.xml dosya tooinclude güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="00b15-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="00b15-202">Ana etkinliklerinizi Authenticationcontext'i örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00b15-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="00b15-203">Bu çağrıyı Hello ayrıntılarını olan bu konuda hello kapsamı dışındadır, ancak hello bakarak iyi bir başlangıç alabilirsiniz [Android Native Client örnek](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="00b15-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="00b15-204">Aşağıdaki örneğine hello SharedPreferences hello varsayılan önbellek ve yetkilisi hello biçiminde `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="00b15-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="00b15-205">Hello kullanıcı kimlik bilgilerini girer ve bir kimlik doğrulama kodu aldıktan sonra bu kodu blok toohandle hello sonuna AuthenticationActivity Kopyala:</span><span class="sxs-lookup"><span data-stu-id="00b15-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="00b15-206">tooask bir belirteci için bir geri çağırma tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="00b15-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="00b15-207">Son olarak, bu geri çağırma kullanarak için bir belirteç isteyin:</span><span class="sxs-lookup"><span data-stu-id="00b15-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="00b15-208">Merhaba parametreleri açıklaması aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="00b15-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="00b15-209">*Kaynak* gereklidir ve tooaccess çalıştığınız hello kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="00b15-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="00b15-210">*ClientID* gereklidir ve Azure AD gelir.</span><span class="sxs-lookup"><span data-stu-id="00b15-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="00b15-211">*RedirectUri* değil hello acquireToken çağrısı için sağlanan gerekli toobe.</span><span class="sxs-lookup"><span data-stu-id="00b15-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="00b15-212">Bu, paket adı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="00b15-213">*PromptBehavior* tooask kimlik bilgileri tooskip hello önbellek ve tanımlama bilgisi için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="00b15-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="00b15-214">*geri çağırma* hello yetkilendirme kodu için bir belirteç değiştirilir sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="00b15-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="00b15-215">Erişim belirteci sahip yazılımdan AuthenticationResult nesne varsa, tarih süresi ve belirteç bilgileri kimliği.</span><span class="sxs-lookup"><span data-stu-id="00b15-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="00b15-216">*acquireTokenSilent* isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="00b15-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="00b15-217">Toohandle önbelleğe alma ve belirteç yenileme çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="00b15-218">Ayrıca, hello eşitleme sürümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-218">It also provides hello sync version.</span></span> <span data-ttu-id="00b15-219">Kabul ettiği *UserID* bir parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="00b15-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="00b15-220">Bu kılavuzu kullanarak, hangi toosuccessfully Azure Active Directory ile tümleştirmeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="00b15-221">Bu çalışma daha fazla örnek için hello AzureADSamples ziyaret / github'daki.</span><span class="sxs-lookup"><span data-stu-id="00b15-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="00b15-222">Önemli bilgiler</span><span class="sxs-lookup"><span data-stu-id="00b15-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="00b15-223">Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="00b15-223">Customization</span></span>
<span data-ttu-id="00b15-224">Uygulama kaynakları kitaplığı proje kaynakları üzerine yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="00b15-225">Bu, uygulamanızın yerleşik ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="00b15-225">This happens when your app is being built.</span></span> <span data-ttu-id="00b15-226">Bu nedenle, istediğiniz kimlik doğrulama etkinliği düzeni hello biçimde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="00b15-227">Merhaba denetimleri emin tookeep hello Kimliğini olması, ADAL (WebView) kullanır.</span><span class="sxs-lookup"><span data-stu-id="00b15-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="00b15-228">Aracısı</span><span class="sxs-lookup"><span data-stu-id="00b15-228">Broker</span></span>
<span data-ttu-id="00b15-229">Merhaba Microsoft Intune Şirket portalı uygulamasını hello Aracısı bileşeni sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="00b15-230">Merhaba hesap AccountManager içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="00b15-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="00b15-231">Merhaba hesap türüdür "com.microsoft.workaccount."</span><span class="sxs-lookup"><span data-stu-id="00b15-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="00b15-232">Yalnızca tek bir SSO hesaba AccountManager sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="00b15-233">Bir hello uygulama için hello aygıt sınaması tamamladıktan sonra hello kullanıcı için bir SSO tanımlama bilgisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00b15-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="00b15-234">ADAL, bir kullanıcı hesabı, bu kimlik doğrulayıcı oluşturulur ve değil tooskip seçerseniz hello aracısı hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="00b15-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="00b15-235">Merhaba Aracısı kullanıcıyla atlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00b15-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="00b15-236">Tooregister özel RedirectUri Aracısı kullanımı için gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="00b15-237">RedirectUri hello biçiminde olduğunu `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="00b15-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="00b15-238">Merhaba betik brokerRedirectPrint.ps1 veya hello API çağrısı mContext.getBrokerRedirectUri kullanarak uygulamanız için RedirectUri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="00b15-239">Merhaba imza imzalama sertifikalarının ilgili tooyour değil.</span><span class="sxs-lookup"><span data-stu-id="00b15-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="00b15-240">Merhaba geçerli aracısı için bir kullanıcı modelidir.</span><span class="sxs-lookup"><span data-stu-id="00b15-240">hello current broker model is for one user.</span></span> <span data-ttu-id="00b15-241">Authenticationcontext'i hello API yöntemi tooget hello Aracısı kullanıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="00b15-242">Uygulama bildiriminizi izinleri toouse AccountManager hesapları aşağıdaki hello olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="00b15-243">Merhaba Ayrıntılar için bkz [hello Android sitesinde AccountManager bilgileri](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="00b15-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="00b15-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="00b15-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="00b15-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="00b15-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="00b15-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="00b15-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="00b15-247">Yetkili URL'si ve AD FS</span><span class="sxs-lookup"><span data-stu-id="00b15-247">Authority URL and AD FS</span></span>
<span data-ttu-id="00b15-248">Hello Authenticationcontext'i Oluşturucusu false değerini iletir ve örnek bulma tooturn gerekir böylece active Directory Federasyon Hizmetleri (AD FS) STS, üretim tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="00b15-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="00b15-249">Merhaba yetkili URL'si STS örneği gerekir ve bir [Kiracı adı](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="00b15-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="00b15-250">Önbellek öğelerini sorgulama</span><span class="sxs-lookup"><span data-stu-id="00b15-250">Querying cache items</span></span>
<span data-ttu-id="00b15-251">ADAL SharedPreferences bazı basit önbelleği ile bir varsayılan önbellekte sorgu işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="00b15-252">Kullanarak Authenticationcontext'i hello güncel önbelleğe alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00b15-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="00b15-253">Toocustomize istiyorsanız, önbellek uygulamanızı de sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="00b15-254">Komut istemi davranışı</span><span class="sxs-lookup"><span data-stu-id="00b15-254">Prompt behavior</span></span>
<span data-ttu-id="00b15-255">ADAL, bir seçenek toospecify komut istemi davranışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="00b15-256">PromptBehavior.Auto hello UI hello yenileme belirteci geçersiz ve kullanıcı kimlik bilgileri gereklidir varsa gösterir.</span><span class="sxs-lookup"><span data-stu-id="00b15-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="00b15-257">PromptBehavior.Always hello önbelleği kullanımını atlayın ve her zaman hello UI gösterir.</span><span class="sxs-lookup"><span data-stu-id="00b15-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="00b15-258">Sessiz belirteç isteği önbellek ve yenileme</span><span class="sxs-lookup"><span data-stu-id="00b15-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="00b15-259">Sessiz bir belirteç isteğini hello UI açılır kullanmaz ve bir etkinlik gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="00b15-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="00b15-260">Bu bir belirteci varsa hello önbellekten döndürür.</span><span class="sxs-lookup"><span data-stu-id="00b15-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="00b15-261">Merhaba belirtecinin süresi varsa, bu yöntem toorefresh çalışır.</span><span class="sxs-lookup"><span data-stu-id="00b15-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="00b15-262">Merhaba yenileme belirtecinin süresi dolmuş ya da başarısız olursa AuthenticationException döndürür.</span><span class="sxs-lookup"><span data-stu-id="00b15-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="00b15-263">Ayrıca, bir eşitleme yapabilirsiniz bu yöntemi kullanarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="00b15-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="00b15-264">Null toocallback ayarlayın veya acquireTokenSilentSync kullanın.</span><span class="sxs-lookup"><span data-stu-id="00b15-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="00b15-265">Tanılama</span><span class="sxs-lookup"><span data-stu-id="00b15-265">Diagnostics</span></span>
<span data-ttu-id="00b15-266">Merhaba birincil bilgi kaynaklarıyla ilgili sorunları tanılamak için bunlar:</span><span class="sxs-lookup"><span data-stu-id="00b15-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="00b15-267">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="00b15-267">Exceptions</span></span>
* <span data-ttu-id="00b15-268">Günlükler</span><span class="sxs-lookup"><span data-stu-id="00b15-268">Logs</span></span>
* <span data-ttu-id="00b15-269">Ağ izlerini</span><span class="sxs-lookup"><span data-stu-id="00b15-269">Network traces</span></span>

<span data-ttu-id="00b15-270">Bağıntı kimlikleri merkezi toohello tanılama hello kitaplığında olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="00b15-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="00b15-271">Bir ADAL isteği kodunuzda diğer işlemlerle toocorrelate istiyorsanız, bir istek başına temelinde bağıntı kimliklerinizi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="00b15-272">Bağıntı kimliği ayarlamazsanız ADAL rastgele bir tane oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00b15-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="00b15-273">Tüm iletileri günlük ve ağ çağrıları sonra hello bağıntı kimliği ile damgalı</span><span class="sxs-lookup"><span data-stu-id="00b15-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="00b15-274">Merhaba her istek kimliği değişiklikleri otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="00b15-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="00b15-275">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="00b15-275">Exceptions</span></span>
<span data-ttu-id="00b15-276">Özel durumları olan hello ilk tanılama.</span><span class="sxs-lookup"><span data-stu-id="00b15-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="00b15-277">Biz tooprovide yararlı hata iletileri deneyin.</span><span class="sxs-lookup"><span data-stu-id="00b15-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="00b15-278">Yararlı olmayan bir fark ederseniz, Lütfen bir sorun dosya ve bize bildirin.</span><span class="sxs-lookup"><span data-stu-id="00b15-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="00b15-279">Model ve SDK numarası gibi cihaz bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="00b15-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="00b15-280">Günlükler</span><span class="sxs-lookup"><span data-stu-id="00b15-280">Logs</span></span>
<span data-ttu-id="00b15-281">Merhaba kitaplığı toogenerate yapılandırabilirsiniz sorunları tanılamak günlük iletilerini toohelp kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="00b15-282">Merhaba aşağıdaki tooconfigure oluşturuldukça ADAL toohand her günlüğü iletisi kapalı kullanacağı bir geri çağırma çağrısı yaparak günlüğe kaydetmeyi yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="00b15-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="00b15-283">İletileri tooa özel günlük dosyası hello kod aşağıdaki gösterildiği gibi yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="00b15-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="00b15-284">Ne yazık ki, bir aygıttan günlüklerini alma standart bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="00b15-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="00b15-285">Bu konuda yardımcı olabilecek bazı hizmetler vardır.</span><span class="sxs-lookup"><span data-stu-id="00b15-285">There are some services that can help you with this.</span></span> <span data-ttu-id="00b15-286">Ayrıca kendi gibi gönderen hello dosya tooa sunucu stok.</span><span class="sxs-lookup"><span data-stu-id="00b15-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="00b15-287">Bunlar hello günlük düzeyleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="00b15-287">These are hello logging levels:</span></span>
* <span data-ttu-id="00b15-288">Hata (özel durumlar)</span><span class="sxs-lookup"><span data-stu-id="00b15-288">Error (exceptions)</span></span>
* <span data-ttu-id="00b15-289">Warn (uyarı)</span><span class="sxs-lookup"><span data-stu-id="00b15-289">Warn (warning)</span></span>
* <span data-ttu-id="00b15-290">Info (bilgilendirme)</span><span class="sxs-lookup"><span data-stu-id="00b15-290">Info (information purposes)</span></span>
* <span data-ttu-id="00b15-291">Verbose (daha fazla ayrıntı)</span><span class="sxs-lookup"><span data-stu-id="00b15-291">Verbose (more details)</span></span>

<span data-ttu-id="00b15-292">Bu gibi hello günlük düzeyini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="00b15-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="00b15-293">Tüm günlük iletilerini toologcat, toplama tooany özel günlük geri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="00b15-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="00b15-294">Bir günlük tooa dosyası logcat aşağıdaki gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00b15-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="00b15-295">Merhaba adb komutları hakkında daha fazla bilgi için bkz [hello Android sitesinde logcat bilgileri](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="00b15-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="00b15-296">Ağ izlerini</span><span class="sxs-lookup"><span data-stu-id="00b15-296">Network traces</span></span>
<span data-ttu-id="00b15-297">ADAL oluşturan çeşitli araçlar toocapture hello HTTP trafiği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="00b15-298">Bu, OAuth protokolünün hello ile aşinaysanız veya tooprovide tanılama bilgileri tooMicrosoft veya diğer destek kanallarını gerekirse en faydalı olur.</span><span class="sxs-lookup"><span data-stu-id="00b15-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="00b15-299">Fiddler hello kolay HTTP izleme aracıdır.</span><span class="sxs-lookup"><span data-stu-id="00b15-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="00b15-300">Kullanım hello aşağıdaki bağlantılar tooset bunun toocorrectly kaydı ADAL ağ trafiği.</span><span class="sxs-lookup"><span data-stu-id="00b15-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="00b15-301">Bir izleme aracı için fiddler'ı veya Charles toobe yararlı gibi şifrelenmemiş toorecord SSL trafiğini yapılandırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="00b15-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="00b15-302">Bu yolla oluşturulan izlemeleri erişim belirteçleri, kullanıcı adları ve parolalar gibi üst düzey ayrıcalıklı bilgileri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="00b15-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="00b15-303">Üretim hesapları kullanıyorsanız, bu izlemelerin üçüncü taraflarla paylaşmayın.</span><span class="sxs-lookup"><span data-stu-id="00b15-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="00b15-304">Toosupply izleme toosomeone sipariş tooget desteğe ihtiyacınız varsa, hello sorunu paylaşma sorun yok geçici bir hesap kullanıcı adlarını ve parolaları kullanarak yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00b15-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="00b15-305">Merhaba Telerik Web sitesinden: [ayarı yukarı Fiddler için Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="00b15-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="00b15-306">Github'dan: [için ADAL Fiddler kurallarını yapılandırma](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="00b15-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="00b15-307">İletişim modu</span><span class="sxs-lookup"><span data-stu-id="00b15-307">Dialog mode</span></span>
<span data-ttu-id="00b15-308">Merhaba acquireToken yöntemi etkinliği olmayan bir iletişim kutusu istemi destekler.</span><span class="sxs-lookup"><span data-stu-id="00b15-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="00b15-309">Şifreleme</span><span class="sxs-lookup"><span data-stu-id="00b15-309">Encryption</span></span>
<span data-ttu-id="00b15-310">ADAL hello belirteçleri ve SharedPreferences deposunda varsayılan olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="00b15-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="00b15-311">Merhaba StorageHelper sınıfı toosee hello ayrıntıları bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="00b15-312">Android 4.3 (API 18) için güvenilir depolama özel anahtarların Android anahtar deposu kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="00b15-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="00b15-313">ADAL, API 18 ve daha yüksek kullanır.</span><span class="sxs-lookup"><span data-stu-id="00b15-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="00b15-314">Daha düşük SDK sürümleri için toouse ADAL istiyorsanız tooprovide AuthenticationSettings.INSTANCE.setSecretKey adresindeki gizli bir anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="00b15-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="00b15-315">OAuth2 taşıyıcı sınama</span><span class="sxs-lookup"><span data-stu-id="00b15-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="00b15-316">Merhaba AuthenticationParameters sınıfı hello OAuth2 taşıyıcı sınama gelen işlevselliği tooget authorization_uri sağlar.</span><span class="sxs-lookup"><span data-stu-id="00b15-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="00b15-317">Web görünümü içinde oturum tanımlama bilgileri</span><span class="sxs-lookup"><span data-stu-id="00b15-317">Session cookies in WebView</span></span>
<span data-ttu-id="00b15-318">Merhaba uygulama kapatıldıktan sonra android WebView oturum tanımlama bilgileri temizlemez.</span><span class="sxs-lookup"><span data-stu-id="00b15-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="00b15-319">Bu örnek kodu kullanarak işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="00b15-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="00b15-320">Tanımlama bilgileri hakkında daha fazla ayrıntı için bkz: Merhaba [hello Android sitesinde CookieSyncManager bilgileri](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="00b15-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="00b15-321">Kaynak geçersiz kılmaları</span><span class="sxs-lookup"><span data-stu-id="00b15-321">Resource overrides</span></span>
<span data-ttu-id="00b15-322">Merhaba ADAL kitaplığı ProgressDialog iletileri için İngilizce dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="00b15-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="00b15-323">Yerelleştirilmiş dizeleri istiyorsanız, uygulamanızın bunları üzerine yazmalıdır.</span><span class="sxs-lookup"><span data-stu-id="00b15-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="00b15-324">NTLM iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="00b15-324">NTLM dialog box</span></span>
<span data-ttu-id="00b15-325">ADAL sürüm 1.1.0 hello onReceivedHttpAuthRequest WebViewClient olayından aracılığıyla işlenen bir NTLM iletişim kutusu destekler.</span><span class="sxs-lookup"><span data-stu-id="00b15-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="00b15-326">Merhaba düzeni ve dizeleri hello iletişim kutusu için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b15-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="00b15-327">Uygulamalar arası SSO'nun</span><span class="sxs-lookup"><span data-stu-id="00b15-327">Cross-app SSO</span></span>
<span data-ttu-id="00b15-328">Bilgi [nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="00b15-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
