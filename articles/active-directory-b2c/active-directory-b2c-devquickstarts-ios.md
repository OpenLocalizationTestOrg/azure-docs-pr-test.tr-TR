---
title: "Bir iOS uygulaması - Azure AD B2C kullanarak bir belirteç alınırken | Microsoft Docs"
description: "Bu makale AppAuth Azure Active Directory B2C ile kullanıcı kimliklerini yönetmek ve kullanıcıların kimliğini doğrulamak için kullandığı bir iOS uygulamasının nasıl oluşturulacağını gösterir."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="437db-103">Azure AD B2C: Bir iOS uygulaması kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="437db-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="437db-104">Microsoft kimlik platformu OAuth2 ve OpenID Connect gibi açık standartlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="437db-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="437db-105">Açık bir standart protokol kullanarak daha fazla Geliştirici seçenekleri hizmetlerimizle tümleştirmek için bir kitaplık seçerken sunar.</span><span class="sxs-lookup"><span data-stu-id="437db-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="437db-106">Bu kılavuzda ve diğerleri gibi Microsoft Identity platformuna bağlanmak uygulamaları yazma ile geliştiricilere yardımcı olmak için sağladık.</span><span class="sxs-lookup"><span data-stu-id="437db-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="437db-107">Uygulayan çoğu kitaplık [RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) Microsoft Identity platformuna bağlanamıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="437db-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="437db-108">Microsoft, üçüncü taraf kitaplıklar için düzeltmeler ve bu kitaplıkları gözden yapılmadı sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="437db-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="437db-109">Bu örnek temel senaryolarda Azure AD B2C ile uyumluluk için test edilmiştir AppAuth adlı bir üçüncü taraf kitaplık kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="437db-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="437db-110">Kitaplığın açık kaynaklı proje yönlendirilmiş sorunları ve özellik istekleri.</span><span class="sxs-lookup"><span data-stu-id="437db-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="437db-111">Daha fazla bilgi için [bu makaleye](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) bakın.</span><span class="sxs-lookup"><span data-stu-id="437db-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="437db-112">OAuth2 veya Openıd Connect kullanmaya yeni başladıysanız Bu örnek yapılandırmanın çoğunu kadar size anlamı olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="437db-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="437db-113">[burada belgelediğimiz protokolün genel bakışına](active-directory-b2c-reference-protocols.md) kısaca bakmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="437db-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="437db-114">Azure AD B2C dizini alma</span><span class="sxs-lookup"><span data-stu-id="437db-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="437db-115">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="437db-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="437db-116">Bir dizin, tüm kullanıcıların, uygulamaları, grupları ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="437db-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="437db-117">Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="437db-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="437db-118">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="437db-118">Create an application</span></span>
<span data-ttu-id="437db-119">Ardından B2C dizininizde uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="437db-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="437db-120">Uygulama kaydı, uygulamanız ile güvenli bir şekilde iletişim kurması için gereken bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="437db-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="437db-121">Mobil bir uygulama oluşturmak için izlemeniz [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="437db-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="437db-122">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="437db-122">Be sure to:</span></span>

* <span data-ttu-id="437db-123">Dahil bir **Native client** uygulamadaki.</span><span class="sxs-lookup"><span data-stu-id="437db-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="437db-124">Uygulamanıza atanan **Uygulama Kimliği**'ni kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="437db-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="437db-125">Bu GUID daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="437db-125">You need this GUID later.</span></span>
* <span data-ttu-id="437db-126">Ayarlanmış bir **yeniden yönlendirme URI'si** özel şema (örneğin, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect) sahip.</span><span class="sxs-lookup"><span data-stu-id="437db-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="437db-127">Bu URI daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="437db-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="437db-128">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="437db-128">Create your policies</span></span>
<span data-ttu-id="437db-129">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="437db-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="437db-130">Bu uygulama bir kimlik deneyimi içerir: bir birleşik oturum açma ve kaydolma.</span><span class="sxs-lookup"><span data-stu-id="437db-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="437db-131">Bu ilkeyi açıklandığı gibi oluşturmak [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="437db-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="437db-132">İlkeyi oluştururken şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="437db-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="437db-133">Altında **kaydolma özniteliklerini**, özniteliği seçin **görünen adı**.</span><span class="sxs-lookup"><span data-stu-id="437db-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="437db-134">Diğer öznitelikler de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="437db-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="437db-135">Altında **uygulama talepleri**, talepleri seçmek **görünen adı** ve **kullanıcının nesne kimliği**.</span><span class="sxs-lookup"><span data-stu-id="437db-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="437db-136">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="437db-136">You can select other claims as well.</span></span>
* <span data-ttu-id="437db-137">Oluşturduktan sonra her ilkenin **Adını** kaydedin.</span><span class="sxs-lookup"><span data-stu-id="437db-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="437db-138">İlke adı önekine sahip `b2c_1_` ilkeyi kaydettiğinizde.</span><span class="sxs-lookup"><span data-stu-id="437db-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="437db-139">İlke adı daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="437db-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="437db-140">İlkelerinizi oluşturduktan sonra uygulamanızı oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="437db-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="437db-141">Örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="437db-141">Download the sample code</span></span>
<span data-ttu-id="437db-142">Azure AD B2C ile AppAuth kullanan bir çalışma örneği sağladık [github'da](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="437db-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="437db-143">Kodu indirin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="437db-143">You can download the code and run it.</span></span> <span data-ttu-id="437db-144">Kendi Azure AD B2C kiracısı kullanmak için ' ndaki yönergeleri izleyin [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="437db-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="437db-145">Bu örnek tarafından Benioku yönergeleri izleyerek oluşturulduğu [iOS AppAuth proje Github'da](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="437db-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="437db-146">Örnek ve kitaplık nasıl çalıştığı hakkında daha fazla ayrıntı için github'da AppAuth Benioku başvuru.</span><span class="sxs-lookup"><span data-stu-id="437db-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="437db-147">Azure AD B2C ile AppAuth kullanmak için uygulamanızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="437db-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="437db-148">AppAuth destekleyen iOS 7 ve üstü.</span><span class="sxs-lookup"><span data-stu-id="437db-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="437db-149">Ancak, sosyal oturum açmalar üzerinde Google desteklemek için SFSafariViewController gereklidir iOS 9 veya üstü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="437db-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="437db-150">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="437db-150">Configuration</span></span>

<span data-ttu-id="437db-151">Yetkilendirme uç noktası ve belirteç uç noktası URI belirterek Azure AD B2C ile iletişim yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="437db-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="437db-152">Bu URI oluşturmak için aşağıdaki bilgiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="437db-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="437db-153">Kiracı kimliği (örneğin, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="437db-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="437db-154">İlke adı (örneğin, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="437db-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="437db-155">Belirteç uç noktası URI Kiracı değiştirerek oluşturulabilir\_kimliği ve ilke\_aşağıdaki URL adı:</span><span class="sxs-lookup"><span data-stu-id="437db-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="437db-156">Kiracı değiştirerek URI oluşturulabilir yetkilendirme uç noktası\_kimliği ve ilke\_aşağıdaki URL adı:</span><span class="sxs-lookup"><span data-stu-id="437db-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="437db-157">AuthorizationServiceConfiguration nesnesi oluşturmak için aşağıdaki kodu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="437db-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="437db-158">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="437db-158">Authorizing</span></span>

<span data-ttu-id="437db-159">Yapılandırma veya bir yetkilendirme hizmet yapılandırmasını alma sonra bir yetkilendirme isteği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="437db-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="437db-160">İsteği oluşturmak için aşağıdaki bilgiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="437db-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="437db-161">İstemci kimliği (örneğin, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="437db-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="437db-162">Özel bir şema ile (örneğin, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect) yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="437db-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="437db-163">Olursa, her iki öğe kaydedildi [uygulamanızı kaydetme](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="437db-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="437db-164">Uygulamanızın yeniden yönlendirme URI'si özel şema ile ayarlamak için Info.pList 'URL şemalarını' listesi güncelleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="437db-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="437db-165">Info.plist açın.</span><span class="sxs-lookup"><span data-stu-id="437db-165">Open Info.pList.</span></span>
* <span data-ttu-id="437db-166">' I tıklatın ve 'Paket işletim sistemi türü kodu' gibi bir satır üzerine gelerek \+ simgesi.</span><span class="sxs-lookup"><span data-stu-id="437db-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="437db-167">Yeni satır 'URL türleri' olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="437db-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="437db-168">'URL türleri' solundaki oka tıklayın ağaç açın.</span><span class="sxs-lookup"><span data-stu-id="437db-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="437db-169">Solundaki oka tıklayın ' 0 ağaç açmak için ' öğesi.</span><span class="sxs-lookup"><span data-stu-id="437db-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="437db-170">'URL şemalarını' 0 öğesine altındaki ilk öğeyi yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="437db-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="437db-171">Ağaç açmak için 'URL şemalarını' solundaki oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="437db-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="437db-172">'Value' sütununda solundaki boş alan yok 'Öğesi 0' 'Altında URL şemalarını'.</span><span class="sxs-lookup"><span data-stu-id="437db-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="437db-173">Değeri, uygulamanızın benzersiz düzenine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="437db-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="437db-174">Değer Redirecturl'yi OIDAuthorizationRequest nesnesi oluşturulurken kullanılan şema eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="437db-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="437db-175">Bizim örnek düzeni 'com.onmicrosoft.fabrikamb2c.exampleapp' kullandık.</span><span class="sxs-lookup"><span data-stu-id="437db-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="437db-176">Başvurmak [AppAuth Kılavuzu](https://openid.github.io/AppAuth-iOS/) işleminin geri kalanında tamamlamak hakkında.</span><span class="sxs-lookup"><span data-stu-id="437db-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="437db-177">Hızlı bir şekilde bir çalışma uygulaması ile çalışmaya başlamak ihtiyacınız varsa kullanıma [bizim örnek](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="437db-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="437db-178">Adımları [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) kendi Azure AD B2C yapılandırma girmek için.</span><span class="sxs-lookup"><span data-stu-id="437db-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="437db-179">Biz her zaman görüş ve öneriler için açık!</span><span class="sxs-lookup"><span data-stu-id="437db-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="437db-180">Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, sayfanın sonundaki görüşlerinize değer veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="437db-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="437db-181">Özellik istekleri için bunları Ekle [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="437db-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
