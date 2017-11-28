---
title: "bir iOS uygulaması içine aaaIntegrate Azure AD | Microsoft Docs"
description: "Nasıl toobuild oturum açma ve Azure AD aramalar için Azure AD ile tümleşen bir iOS uygulaması API'leri OAuth kullanılarak korunan."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="1c15f-103">Azure AD bir iOS uygulamanıza tümleştirmek</span><span class="sxs-lookup"><span data-stu-id="1c15f-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="1c15f-104">Bizim yeni Hello önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/iOS) yardımcı olan Azure Active Directory ile yalnızca birkaç dakika içinde başlamak ve çalıştırmak!</span><span class="sxs-lookup"><span data-stu-id="1c15f-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="1c15f-105">Hello Geliştirici Portalı bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme hello işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="1c15f-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="1c15f-106">İşiniz bittiğinde, bu belirteçleri kabul edebilir ve doğrulama gerçekleştirmek kullanıcılar, Kiracı ve arka uç kimlik doğrulaması yapabilir basit bir uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c15f-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="1c15f-107">Azure Active Directory (Azure AD) tooaccess gereken iOS istemciler korunan kaynakları hello Active Directory kimlik doğrulama kitaplığı ya da ADAL sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c15f-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="1c15f-108">ADAL uygulamanızı tooobtain erişim belirteçleri kullandığını hello işlemini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="1c15f-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="1c15f-109">toodemonstrate olduğu, bu makaledeki ne kadar kolay bir hedefi C Yapılacaklar listesi uygulaması, biz oluşturma:</span><span class="sxs-lookup"><span data-stu-id="1c15f-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="1c15f-110">Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c15f-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="1c15f-111">Belirtilen diğer ada sahip kullanıcılar için bir dizin arar.</span><span class="sxs-lookup"><span data-stu-id="1c15f-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="1c15f-112">toobuild hello tam çalışan bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c15f-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="1c15f-113">Uygulamanızı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1c15f-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="1c15f-114">Yükleyin ve ADAL yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="1c15f-115">Azure AD'den ADAL tooget belirteçleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="1c15f-116">başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1c15f-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="1c15f-117">Ayrıca kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c15f-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="1c15f-118">Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="1c15f-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="1c15f-119">Bizim yeni Hello önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/iOS) yardımcı olan birkaç dakika içinde Azure AD ile başlamak ve çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="1c15f-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="1c15f-120">Hello Geliştirici Portalı bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme hello işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="1c15f-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="1c15f-121">Kullanıcıların kiracınızda doğrulanabilir basit bir uygulamanız varsa ve bir arka uç tamamlanmış olduğunuzda, belirteçleri kabul edebilir ve doğrulama yapmak.</span><span class="sxs-lookup"><span data-stu-id="1c15f-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="1c15f-122">1. İOS için URI'dir, yönlendirme belirleme</span><span class="sxs-lookup"><span data-stu-id="1c15f-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="1c15f-123">toosecurely belirli SSO senaryolarda uygulamalarınızın Başlat, oluşturmanız gerekir bir *yeniden yönlendirme URI'si* belirli bir biçimde.</span><span class="sxs-lookup"><span data-stu-id="1c15f-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="1c15f-124">Bir yeniden yönlendirme URI'si için bunları sorulan belirteçleri dönüş toohello doğru uygulama hello kullanılan tooensure ' dir.</span><span class="sxs-lookup"><span data-stu-id="1c15f-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="1c15f-125">Hello iOS için bir yeniden yönlendirme URI'si biçimdir:</span><span class="sxs-lookup"><span data-stu-id="1c15f-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="1c15f-126">**Uygulama düzeni** -Bu, XCode projenizde kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="1c15f-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="1c15f-127">Bu, nasıl diğer uygulamaları çağırabilirsiniz olur.</span><span class="sxs-lookup"><span data-stu-id="1c15f-127">It is how other applications can call you.</span></span> <span data-ttu-id="1c15f-128">Bulabileceğiniz bu Info.plist altında -> URL türleri -> URL tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1c15f-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="1c15f-129">Bir veya daha fazla yapılandırılmış henüz yoksa bir oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c15f-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="1c15f-130">**paket kimliği** -hello paket "kimlik" altında bulunan tanımlayıcısı budur kaydını proje ayarlarınızı xcode'da.</span><span class="sxs-lookup"><span data-stu-id="1c15f-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="1c15f-131">Bu hızlı başlangıç kodun bir örnek: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="1c15f-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="1c15f-132">2. Merhaba DirectorySearcher uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="1c15f-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="1c15f-133">tooset uygulama tooget belirteçleri yukarı ilk ihtiyacınız tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin:</span><span class="sxs-lookup"><span data-stu-id="1c15f-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="1c15f-134">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c15f-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c15f-135">Merhaba üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-135">On hello top bar, click your account.</span></span> <span data-ttu-id="1c15f-136">Merhaba altında **Directory** listesinde, uygulamanızın hello Active Directory Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="1c15f-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="1c15f-137">Tıklatın **daha Hizmetleri** hello Soldaki gezinti bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c15f-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="1c15f-138">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1c15f-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="1c15f-139">İzleyin hello ister yeni bir toocreate **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="1c15f-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="1c15f-140">Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın açıklar.</span><span class="sxs-lookup"><span data-stu-id="1c15f-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="1c15f-141">Merhaba **yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanan bir şema ve dize birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="1c15f-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="1c15f-142">Belirli tooyour uygulama ve hello önceki yeniden yönlendirme URI'si bilgiyi temel alan bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="1c15f-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="1c15f-143">Merhaba kaydı tamamladıktan sonra Azure AD, uygulamanızın benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="1c15f-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="1c15f-144">Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="1c15f-145">Merhaba gelen **ayarları** sayfasında, **gerekli izinler** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1c15f-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="1c15f-146">Seçin **Microsoft Graph** API, hello gibi hello ekleyin **dizin verilerini okuma** altında izni **izinlere temsilci**.</span><span class="sxs-lookup"><span data-stu-id="1c15f-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="1c15f-147">Bu, kullanıcılar için Azure AD Graph API uygulaması tooquery hello ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1c15f-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="1c15f-148">3. Yükleme ve yapılandırma ADAL</span><span class="sxs-lookup"><span data-stu-id="1c15f-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="1c15f-149">Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="1c15f-150">Azure AD ile ADAL toocommunicate için tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.</span><span class="sxs-lookup"><span data-stu-id="1c15f-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="1c15f-151">CocoaPods kullanarak ADAL toohello DirectorySearcher proje ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="1c15f-152">Toothis podfile aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1c15f-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="1c15f-153">Şimdi CocoaPods kullanarak hello podfile dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1c15f-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="1c15f-154">Bu adım, yüklediğiniz yeni bir XCode çalışma alanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1c15f-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="1c15f-155">Merhaba hızlı başlangıç projesi hello plist dosyasını açın `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="1c15f-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="1c15f-156">Hello Azure portal girdiğiniz hello bölüm tooreflect hello değerleri hello öğelerinde Hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1c15f-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="1c15f-157">ADAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="1c15f-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="1c15f-158">Merhaba `tenant` Azure AD kiracınız, örneğin, contoso.onmicrosoft.com hello etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="1c15f-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="1c15f-159">Merhaba `clientId` hello portalından kopyalandığından, uygulamanızın hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c15f-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="1c15f-160">Merhaba `redirectUri` hello Portalı'nda kayıtlı hello yeniden yönlendirme URL'si.</span><span class="sxs-lookup"><span data-stu-id="1c15f-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="1c15f-161">4.    Azure AD'den ADAL tooget belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="1c15f-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="1c15f-162">Merhaba temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, bu yalnızca bir completionBlock çağırdığı ilkesidir `+(void) getToken : `, ve ADAL rest hello.</span><span class="sxs-lookup"><span data-stu-id="1c15f-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="1c15f-163">Merhaba, `QuickStart` proje, açık `GraphAPICaller.m` ve hello bulun `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` hello üstüne yakın açıklama.</span><span class="sxs-lookup"><span data-stu-id="1c15f-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="1c15f-164">Burada ADAL hello koordinatları CompletionBlock, Azure AD ile toocommunicate aracılığıyla geçirmek ve nasıl söyleyin budur toocache belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="1c15f-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="1c15f-165">Şimdi toouse Bu belirteci toosearch hello grafik alanındaki kullanıcılar için ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="1c15f-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="1c15f-166">Hello bulur `// TODO: implement SearchUsersList` açıklama.</span><span class="sxs-lookup"><span data-stu-id="1c15f-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="1c15f-167">Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir GET isteği toohello Azure AD Graph API tooquery sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c15f-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="1c15f-168">tooquery hello Azure AD grafik API'si, gereksinim duyduğunuz tooinclude bir access_token ile Merhaba `Authorization` hello isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="1c15f-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="1c15f-169">ADAL nereden geldiğini budur.</span><span class="sxs-lookup"><span data-stu-id="1c15f-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. <span data-ttu-id="1c15f-170">Uygulamanızı isteğinde bulunduğunda bir belirteç çağırarak `getToken(...)`, ADAL tooreturn bir belirteç hello kullanıcı kimlik bilgilerinin sorulmasına olmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="1c15f-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="1c15f-171">ADAL tooget bir belirteç toosign hello kullanıcı gerektiğini belirlerse, oturum açma için bir iletişim kutusu görüntüler, hello kullanıcının kimlik bilgilerini toplamak ve sonra bir belirteç başarılı kimlik doğrulamasından sonra geri dönüp.</span><span class="sxs-lookup"><span data-stu-id="1c15f-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="1c15f-172">ADAL mümkün tooreturn bir belirteç herhangi bir nedenle değilse oluşturur bir `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="1c15f-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="1c15f-173">Merhaba `AuthenticationResult` nesnesini içeren bir `tokenCacheStoreItem` uygulamanız gerekebilir kullanılan toocollect hello bilgi olabilir nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1c15f-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="1c15f-174">Merhaba hızlı başlangıç, içinde `tokenCacheStoreItem` kullanılan toodetermine ise kimlik doğrulaması zaten yapıldı.</span><span class="sxs-lookup"><span data-stu-id="1c15f-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="1c15f-175">5. Derleme ve Merhaba uygulaması çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1c15f-175">5. Build and run hello application</span></span>
<span data-ttu-id="1c15f-176">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="1c15f-176">Congratulations!</span></span> <span data-ttu-id="1c15f-177">Artık çalışan bir iOS uygulama kullanıcıların kimlik doğrulaması, güvenli bir şekilde OAuth 2.0 kullanarak Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri elde var.</span><span class="sxs-lookup"><span data-stu-id="1c15f-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="1c15f-178">Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1c15f-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="1c15f-179">Hızlı Başlangıç uygulamanızı başlatın ve ardından kullanıcılar bir oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="1c15f-180">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="1c15f-181">Merhaba uygulamayı kapatın ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1c15f-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="1c15f-182">Merhaba kullanıcının oturumunu değişmeden kalır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1c15f-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="1c15f-183">ADAL kolay tooincorporate kılar uygulamanıza bu ortak kimlik özelliklerin tümü.</span><span class="sxs-lookup"><span data-stu-id="1c15f-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="1c15f-184">Bunu tüm hello dirty çalışmanın sizin için önbellek yönetimi gibi OAuth protokol desteği ile bir kullanıcı Arabirimi toosign hello kullanıcı sunan ve belirteçlerin süresinin yenileme mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="1c15f-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="1c15f-185">Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `getToken`.</span><span class="sxs-lookup"><span data-stu-id="1c15f-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="1c15f-186">Başvuru için üzerinde tamamlandı hello örnek (yapılandırma değerleriniz olmadan) sağlanır [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1c15f-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1c15f-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c15f-187">Next steps</span></span>
<span data-ttu-id="1c15f-188">Şimdi tooadditional senaryoları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c15f-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="1c15f-189">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1c15f-189">You may want tootry:</span></span>

* [<span data-ttu-id="1c15f-190">Node.JS Web API'si Azure AD ile güvenli</span><span class="sxs-lookup"><span data-stu-id="1c15f-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="1c15f-191">Bilgi [nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak iOS](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="1c15f-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

