---
title: "Bir iOS uygulaması - Azure AD B2C kullanarak bir belirteç alınırken | Microsoft Docs"
description: "Bu makale size nasıl gösterir toocreate Azure Active Directory B2C toomanage kullanıcı kimliklerle AppAuth kullanır ve kullanıcıların kimliklerini bir iOS uygulaması."
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
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="d4751-103">Azure AD B2C: Bir iOS uygulaması kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="d4751-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="d4751-104">Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4751-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="d4751-105">Açık bir standart protokol kullanarak, bir kitaplık toointegrate hizmetlerimizle ile seçerken daha fazla Geliştirici seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="d4751-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="d4751-106">Bu kılavuzda ve diğerleri gibi tooaid geliştiriciler toohello Microsoft Identity platform bağlanan uygulamaları yazma ile sağladık.</span><span class="sxs-lookup"><span data-stu-id="d4751-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="d4751-107">Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) mümkün tooconnect toohello Microsoft Identity platformu olan.</span><span class="sxs-lookup"><span data-stu-id="d4751-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="d4751-108">Microsoft, üçüncü taraf kitaplıklar için düzeltmeler ve bu kitaplıkları gözden yapılmadı sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="d4751-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="d4751-109">Bu örnek temel senaryolarda hello Azure AD B2C ile uyumluluk için test edilmiştir AppAuth adlı bir üçüncü taraf kitaplık kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="d4751-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="d4751-110">Sorunları ve özellik istekleri yönlendirilmiş toohello kitaplığın açık kaynaklı proje olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4751-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="d4751-111">Daha fazla bilgi için [bu makaleye](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) bakın.</span><span class="sxs-lookup"><span data-stu-id="d4751-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="d4751-112">Yeni tooOAuth2 veya Openıd Connect değilseniz, bu örnek yapılandırmanın çoğunu kadar algılama tooyou oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="d4751-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="d4751-113">Kısaca öneririz [biz burada belgelediğimiz hello protokolüne genel bakış](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d4751-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="d4751-114">Azure AD B2C dizini alma</span><span class="sxs-lookup"><span data-stu-id="d4751-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="d4751-115">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4751-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="d4751-116">Bir dizin, tüm kullanıcıların, uygulamaları, grupları ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d4751-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="d4751-117">Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d4751-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="d4751-118">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4751-118">Create an application</span></span>
<span data-ttu-id="d4751-119">Ardından B2C dizininizde uygulama toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4751-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="d4751-120">Hello uygulama kaydı, uygulamanız ile güvenli toocommunicate gereken bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="d4751-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="d4751-121">bir mobil uygulama toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d4751-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="d4751-122">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="d4751-122">Be sure to:</span></span>

* <span data-ttu-id="d4751-123">Dahil bir **Native client** hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="d4751-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="d4751-124">Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="d4751-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="d4751-125">Bu GUID daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4751-125">You need this GUID later.</span></span>
* <span data-ttu-id="d4751-126">Ayarlanmış bir **yeniden yönlendirme URI'si** özel şema (örneğin, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect) sahip.</span><span class="sxs-lookup"><span data-stu-id="d4751-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="d4751-127">Bu URI daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4751-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="d4751-128">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4751-128">Create your policies</span></span>
<span data-ttu-id="d4751-129">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d4751-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d4751-130">Bu uygulama bir kimlik deneyimi içerir: bir birleşik oturum açma ve kaydolma.</span><span class="sxs-lookup"><span data-stu-id="d4751-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="d4751-131">Bu ilkeyi açıklandığı gibi oluşturmak [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="d4751-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="d4751-132">Hello ilkesi oluşturduğunuzda, emin olun:</span><span class="sxs-lookup"><span data-stu-id="d4751-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="d4751-133">Altında **kaydolma özniteliklerini**seçin hello özniteliği **görünen adı**.</span><span class="sxs-lookup"><span data-stu-id="d4751-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="d4751-134">Diğer öznitelikler de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4751-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="d4751-135">Altında **uygulama talepleri**, seçin hello talep **görünen adı** ve **kullanıcının nesne kimliği**.</span><span class="sxs-lookup"><span data-stu-id="d4751-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="d4751-136">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4751-136">You can select other claims as well.</span></span>
* <span data-ttu-id="d4751-137">Kopya hello **adı** oluşturduktan sonra her ilkenin.</span><span class="sxs-lookup"><span data-stu-id="d4751-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="d4751-138">İlke adı önekine sahip `b2c_1_` hello İlkesi kaydettiğinizde.</span><span class="sxs-lookup"><span data-stu-id="d4751-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="d4751-139">Hello ilkesi adı daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4751-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="d4751-140">İlkelerinizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="d4751-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="d4751-141">Merhaba örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="d4751-141">Download hello sample code</span></span>
<span data-ttu-id="d4751-142">Azure AD B2C ile AppAuth kullanan bir çalışma örneği sağladık [github'da](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d4751-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="d4751-143">Merhaba kodu indirin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d4751-143">You can download hello code and run it.</span></span> <span data-ttu-id="d4751-144">toouse kendi Azure AD B2C Kiracı, hello hello yönergeleri izleyin [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d4751-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="d4751-145">Bu örnek tarafından hello hello Benioku yönergeleri izleyerek oluşturulduğu [iOS AppAuth proje Github'da](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="d4751-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="d4751-146">Hello örnek ve hello kitaplığı nasıl çalıştığı hakkında daha fazla ayrıntı için github'da AppAuth Benioku hello başvuru.</span><span class="sxs-lookup"><span data-stu-id="d4751-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="d4751-147">Uygulama toouse Azure AD B2C AppAuth ile değiştirme</span><span class="sxs-lookup"><span data-stu-id="d4751-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="d4751-148">AppAuth destekleyen iOS 7 ve üstü.</span><span class="sxs-lookup"><span data-stu-id="d4751-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="d4751-149">Ancak, Google, SFSafariViewController toosupport sosyal oturum gereklidir iOS 9 veya üstü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4751-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="d4751-150">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4751-150">Configuration</span></span>

<span data-ttu-id="d4751-151">Merhaba yetkilendirme uç noktası ve belirteç uç noktası URI belirterek Azure AD B2C ile iletişim yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4751-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="d4751-152">toogenerate bu URI bilgisinden hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4751-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="d4751-153">Kiracı kimliği (örneğin, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="d4751-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="d4751-154">İlke adı (örneğin, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="d4751-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="d4751-155">Merhaba belirteç uç noktası URI değiştirerek oluşturulabilir hello Kiracı\_kimliği ve hello İlkesi\_URL aşağıdaki hello adı:</span><span class="sxs-lookup"><span data-stu-id="d4751-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="d4751-156">Merhaba yetkilendirme uç noktası URI değiştirerek oluşturulabilir hello Kiracı\_kimliği ve hello İlkesi\_URL aşağıdaki hello adı:</span><span class="sxs-lookup"><span data-stu-id="d4751-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="d4751-157">Aşağıdaki kod toocreate hello AuthorizationServiceConfiguration nesnenizin çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d4751-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="d4751-158">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="d4751-158">Authorizing</span></span>

<span data-ttu-id="d4751-159">Yapılandırma veya bir yetkilendirme hizmet yapılandırmasını alma sonra bir yetkilendirme isteği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="d4751-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="d4751-160">toocreate hello istek bilgisinden hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4751-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="d4751-161">İstemci kimliği (örneğin, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="d4751-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="d4751-162">Özel bir şema ile (örneğin, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect) yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="d4751-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="d4751-163">Olursa, her iki öğe kaydedildi [uygulamanızı kaydetme](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="d4751-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="d4751-164">tooset, uygulama toohandle hello yeniden yönlendirme toohello URI hello özel şema ile yukarı Info.pList dosyasında tooupdate hello 'URL şemalarını' listesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4751-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="d4751-165">Info.plist açın.</span><span class="sxs-lookup"><span data-stu-id="d4751-165">Open Info.pList.</span></span>
* <span data-ttu-id="d4751-166">'Paket işletim sistemi türü kodu' gibi bir satır üzerine gelerek ve hello tıklatın \+ simgesi.</span><span class="sxs-lookup"><span data-stu-id="d4751-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="d4751-167">Merhaba yeni satır 'URL türleri' olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="d4751-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="d4751-168">'URL türleri' tooopen hello ağacının Hello ok toohello sol tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4751-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="d4751-169">'0 öğe' tooopen hello ağacının Hello ok toohello sol tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4751-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="d4751-170">İlk öğeyi öğesi 0 too'URL düzenleri altında yeniden adlandırmak.</span><span class="sxs-lookup"><span data-stu-id="d4751-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="d4751-171">'URL şemalarını' tooopen hello ağacının Hello ok toohello sol tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4751-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="d4751-172">Merhaba 'Value' sütununda bir boş alan toohello solundaki yok 'Öğesi 0' 'Altında URL şemalarını'.</span><span class="sxs-lookup"><span data-stu-id="d4751-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="d4751-173">Merhaba değeri tooyour uygulamanın benzersiz düzeni ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d4751-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="d4751-174">Merhaba değeri içinde Redirecturl'yi hello OIDAuthorizationRequest nesnesi oluşturulurken kullanılan hello şeması eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="d4751-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="d4751-175">Bizim örnek hello düzeni 'com.onmicrosoft.fabrikamb2c.exampleapp' kullandık.</span><span class="sxs-lookup"><span data-stu-id="d4751-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="d4751-176">Toohello başvuran [AppAuth Kılavuzu](https://openid.github.io/AppAuth-iOS/) nasıl toocomplete hello hello işleminin geri kalanında üzerinde.</span><span class="sxs-lookup"><span data-stu-id="d4751-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="d4751-177">Tooquickly gerekiyorsa bir çalışma uygulaması ile çalışmaya başlama, kullanıma [bizim örnek](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d4751-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="d4751-178">Merhaba Hello adımları [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter kendi Azure AD B2C yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="d4751-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="d4751-179">Her zaman açık toofeedback ve öneriler duyuyoruz!</span><span class="sxs-lookup"><span data-stu-id="d4751-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="d4751-180">Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, hello sayfanın hello sonundaki görüşlerinize değer veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="d4751-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="d4751-181">Özellik istekleri için çok eklemediğiniz[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="d4751-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
