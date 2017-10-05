---
title: "Azure AD bir iOS uygulamanıza tümleştirmek | Microsoft Docs"
description: "Oturum açma ve Azure AD aramalar için Azure AD ile tümleşen bir iOS uygulamasının nasıl oluşturulacağını, OAuth kullanılarak API'leri korunan."
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
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="5b885-103">Azure AD bir iOS uygulamanıza tümleştirmek</span><span class="sxs-lookup"><span data-stu-id="5b885-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="5b885-104">Bizim yeni önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/iOS) yardımcı olan Azure Active Directory ile yalnızca birkaç dakika içinde başlamak ve çalıştırmak!</span><span class="sxs-lookup"><span data-stu-id="5b885-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="5b885-105">Geliştirici Portalı bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="5b885-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="5b885-106">İşiniz bittiğinde, bu belirteçleri kabul edebilir ve doğrulama gerçekleştirmek kullanıcılar, Kiracı ve arka uç kimlik doğrulaması yapabilir basit bir uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b885-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="5b885-107">Azure Active Directory (Azure AD), korunan kaynaklara erişim için gereken iOS istemciler için Active Directory kimlik doğrulama kitaplığı ya da ADAL sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b885-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="5b885-108">ADAL erişim belirteci edinmek için uygulamanızın kullandığı işlemini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="5b885-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="5b885-109">Ne kadar kolay olduğunu, göstermek için bu makaledeki biz bir hedefi C Yapılacaklar listesi uygulaması, oluşturma:</span><span class="sxs-lookup"><span data-stu-id="5b885-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="5b885-110">Alır erişim belirteçleri kullanarak Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b885-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="5b885-111">Belirtilen diğer ada sahip kullanıcılar için bir dizin arar.</span><span class="sxs-lookup"><span data-stu-id="5b885-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="5b885-112">Tam çalışan uygulama oluşturmak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b885-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="5b885-113">Uygulamanızı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5b885-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="5b885-114">Yükleyin ve ADAL yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5b885-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="5b885-115">ADAL, Azure AD'den belirteçleri almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b885-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="5b885-116">Başlamak için [uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) veya [tamamlanan örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5b885-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="5b885-117">Ayrıca kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b885-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="5b885-118">Bir kiracı yoksa [edinebileceğinizi öğrenin](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5b885-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="5b885-119">Bizim yeni önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/iOS) yardımcı olan birkaç dakika içinde Azure AD ile başlamak ve çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="5b885-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="5b885-120">Geliştirici Portalı bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="5b885-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="5b885-121">Kullanıcıların kiracınızda doğrulanabilir basit bir uygulamanız varsa ve bir arka uç tamamlanmış olduğunuzda, belirteçleri kabul edebilir ve doğrulama yapmak.</span><span class="sxs-lookup"><span data-stu-id="5b885-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="5b885-122">1. İOS için URI'dir, yönlendirme belirleme</span><span class="sxs-lookup"><span data-stu-id="5b885-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="5b885-123">Güvenli bir şekilde uygulamalarınızın belirli SSO senaryolarda başlatmak için oluşturmalısınız bir *yeniden yönlendirme URI'si* belirli bir biçimde.</span><span class="sxs-lookup"><span data-stu-id="5b885-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="5b885-124">Yeniden yönlendirme URI'si belirteçleri kendileri için sorulan doğru uygulama dönmek emin olmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b885-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="5b885-125">İOS için bir yeniden yönlendirme URI'si biçimidir:</span><span class="sxs-lookup"><span data-stu-id="5b885-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="5b885-126">**Uygulama düzeni** -Bu, XCode projenizde kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="5b885-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="5b885-127">Bu, nasıl diğer uygulamaları çağırabilirsiniz olur.</span><span class="sxs-lookup"><span data-stu-id="5b885-127">It is how other applications can call you.</span></span> <span data-ttu-id="5b885-128">Bulabileceğiniz bu Info.plist altında -> URL türleri -> URL tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5b885-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="5b885-129">Bir veya daha fazla yapılandırılmış henüz yoksa bir oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b885-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="5b885-130">**paket kimliği** -bu paket "kimlik" altında bulunan tanımlayıcısıdır kaydını proje ayarlarınızı xcode'da.</span><span class="sxs-lookup"><span data-stu-id="5b885-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="5b885-131">Bu hızlı başlangıç kodun bir örnek: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="5b885-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="5b885-132">2. DirectorySearcher uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="5b885-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="5b885-133">Belirteçleri almak için uygulamanızı ayarlayın için önce Azure AD kiracınızda kaydolun ve Azure AD grafik API'sine erişim izni vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b885-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="5b885-134">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5b885-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5b885-135">Üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5b885-135">On the top bar, click your account.</span></span> <span data-ttu-id="5b885-136">Altında **Directory** listesinde, Active Directory Kiracı uygulamanızı kaydetmek istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="5b885-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="5b885-137">Tıklatın **daha Hizmetleri** Soldaki gezinti bölmesi ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b885-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5b885-138">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5b885-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="5b885-139">Yeni bir oluşturmak için istemleri izleyin **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="5b885-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="5b885-140">**Adı** uygulamanızı son kullanıcıların uygulamayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="5b885-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="5b885-141">**Yeniden yönlendirme URI'si** belirteci yanıtları döndürmek için Azure AD kullanır ve dize şeması bir birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="5b885-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="5b885-142">Uygulamanıza özeldir ve önceki yeniden yönlendirme URI'si bilgiyi temel alan bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="5b885-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="5b885-143">Azure AD kaydı'nı tamamladıktan sonra uygulamanızı bir benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="5b885-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="5b885-144">Bu değer gerekir sonraki bölümlerde, bu nedenle uygulama sekmesinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5b885-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="5b885-145">Gelen **ayarları** sayfasında, **gerekli izinler** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5b885-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="5b885-146">Seçin **Microsoft Graph** API olarak ve ardından ekleyin **dizin verilerini okuma** altında izni **izinlere temsilci**.</span><span class="sxs-lookup"><span data-stu-id="5b885-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="5b885-147">Bu kullanıcılar için Azure AD Graph API sorgulamak için uygulamanızı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5b885-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="5b885-148">3. Yükleme ve yapılandırma ADAL</span><span class="sxs-lookup"><span data-stu-id="5b885-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="5b885-149">Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="5b885-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="5b885-150">Azure AD ile iletişim kurmak ADAL için uygulama kaydınızı hakkında bazı bilgiler ile sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b885-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="5b885-151">CocoaPods kullanarak ADAL DirectorySearcher projeye ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="5b885-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="5b885-152">Aşağıdakileri bu podfile dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5b885-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="5b885-153">Şimdi CocoaPods kullanarak podfile dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5b885-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="5b885-154">Bu adım, yüklediğiniz yeni bir XCode çalışma alanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b885-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="5b885-155">Hızlı başlangıç projesi plist dosyasını açın `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="5b885-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="5b885-156">Azure portalında girdiğiniz değerleri yansıtacak şekilde bölümdeki öğelerinin değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5b885-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="5b885-157">ADAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="5b885-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="5b885-158">`tenant` Azure AD kiracınız, örneğin, contoso.onmicrosoft.com etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="5b885-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="5b885-159">`clientId` Portalından kopyalandığından, uygulamanızın istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="5b885-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="5b885-160">`redirectUri` Portalı'nda kayıtlı yeniden yönlendirme URL'si.</span><span class="sxs-lookup"><span data-stu-id="5b885-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="5b885-161">4.    Azure AD'den belirteçleri almak için ADAL'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="5b885-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="5b885-162">Temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, bu yalnızca bir completionBlock çağırdığı ilkesidir `+(void) getToken : `, ve ADAL rest yapar.</span><span class="sxs-lookup"><span data-stu-id="5b885-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="5b885-163">İçinde `QuickStart` proje, açık `GraphAPICaller.m` ve bulun `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` ilk açıklama.</span><span class="sxs-lookup"><span data-stu-id="5b885-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="5b885-164">ADAL burada geçirdiğiniz budur Azure AD ile iletişim kurmak ve belirteçleri önbelleğe almak nasıl bildirmek için bir CompletionBlock aracılığıyla koordinatları.</span><span class="sxs-lookup"><span data-stu-id="5b885-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="5b885-165">Şimdi biz grafikte kullanıcıları aramak için bu belirteci kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b885-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="5b885-166">Bul `// TODO: implement SearchUsersList` açıklama.</span><span class="sxs-lookup"><span data-stu-id="5b885-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="5b885-167">Bu yöntem, UPN verilen arama terimiyle kullanıcıları için Azure AD Graph API sorgu için bir GET isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="5b885-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="5b885-168">Azure AD Graph API sorgulamak için bir access_token ile eklemeniz gerekir `Authorization` isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="5b885-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="5b885-169">ADAL nereden geldiğini budur.</span><span class="sxs-lookup"><span data-stu-id="5b885-169">This is where ADAL comes in.</span></span>

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

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
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


3. <span data-ttu-id="5b885-170">Uygulamanızı isteğinde bulunduğunda bir belirteç çağırarak `getToken(...)`, ADAL kullanıcı kimlik bilgilerinin sorulmasına olmadan bir simge döndürür dener.</span><span class="sxs-lookup"><span data-stu-id="5b885-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="5b885-171">ADAL kullanıcı bir belirteç almak üzere oturum açmak gerektiğini belirlerse, oturum açma için bir iletişim kutusu görüntüler, kullanıcının kimlik bilgilerini toplamak ve sonra bir belirteç başarılı kimlik doğrulamasından sonra geri dönüp.</span><span class="sxs-lookup"><span data-stu-id="5b885-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="5b885-172">ADAL herhangi bir nedenle bir simge döndürür mümkün değilse, oluşturur bir `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="5b885-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="5b885-173">`AuthenticationResult` Nesnesini içeren bir `tokenCacheStoreItem` uygulamanız gerekebilir bilgi toplamak için kullanılan nesne.</span><span class="sxs-lookup"><span data-stu-id="5b885-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="5b885-174">Hızlı Başlangıç içinde `tokenCacheStoreItem` kimlik doğrulamanın zaten yapılıp belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b885-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="5b885-175">5. Uygulamayı derleme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5b885-175">5. Build and run the application</span></span>
<span data-ttu-id="5b885-176">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="5b885-176">Congratulations!</span></span> <span data-ttu-id="5b885-177">Artık çalışan bir iOS uygulama kullanıcıların kimlik doğrulaması, güvenli bir şekilde OAuth 2.0 kullanarak Web API'leri çağırmak ve kullanıcı hakkındaki temel bilgileri elde var.</span><span class="sxs-lookup"><span data-stu-id="5b885-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="5b885-178">Henüz yapmadıysanız, bazı kullanıcılar ile Kiracı doldurmak için zaman sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="5b885-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="5b885-179">Hızlı Başlangıç uygulamanızı başlatın ve ardından kullanıcılar bir oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5b885-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="5b885-180">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="5b885-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="5b885-181">Uygulamayı kapatın ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="5b885-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="5b885-182">Kullanıcının oturumunu değişmeden kalır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5b885-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="5b885-183">ADAL, bu ortak kimlik özelliklerin tümü, uygulamanıza eklemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5b885-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="5b885-184">Bu tüm dirty iş sizin için önbellek yönetimi gibi OAuth protokol desteği, kullanıcı oturum açma, için bir kullanıcı Arabirimi ile sunan mvc'deki ve yenileme belirteçleri süresi.</span><span class="sxs-lookup"><span data-stu-id="5b885-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="5b885-185">Gerçekten bilmeniz gereken tek şey tek bir API çağrısı `getToken`.</span><span class="sxs-lookup"><span data-stu-id="5b885-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="5b885-186">Başvuru için üzerinde tamamlanan örnek (yapılandırma değerleriniz olmadan) sağlanır [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5b885-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="5b885-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b885-187">Next steps</span></span>
<span data-ttu-id="5b885-188">Şimdi ilave senaryolar da taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b885-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="5b885-189">Denemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b885-189">You may want to try:</span></span>

* [<span data-ttu-id="5b885-190">Node.JS Web API'si Azure AD ile güvenli</span><span class="sxs-lookup"><span data-stu-id="5b885-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="5b885-191">Bilgi [uygulamalar arası SSO'nun ADAL kullanarak iOS etkinleştirme](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="5b885-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

