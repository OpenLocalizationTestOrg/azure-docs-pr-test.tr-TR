---
title: "Azure Active Directory B2C: bir Android uygulamasını kullanarak bir belirteç alınırken | Microsoft Docs"
description: "Bu makale AppAuth Azure Active Directory B2C ile kullanıcı kimliklerini yönetmek ve kullanıcıların kimliğini doğrulamak için kullandığı bir Android uygulamasının nasıl oluşturulacağını gösterir."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="59c61-103">Azure AD B2C: Bir Android uygulamasını kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="59c61-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="59c61-104">Microsoft kimlik platformu OAuth2 ve OpenID Connect gibi açık standartlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="59c61-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="59c61-105">Bunun yapılması geliştiricilerin hizmetlerimizle tümleştirmek istediği herhangi bir kitaplıktan yararlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="59c61-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="59c61-106">Geliştiricilerin platformumuzu diğer kitaplıklarla birlikte kullanmasına yardımcı olmak için 3 taraf kitaplıkların Microsoft identity platformuna bağlanmak için yapılandırma göstermek için bunun gibi birkaç izlenecek yazdıktan.</span><span class="sxs-lookup"><span data-stu-id="59c61-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="59c61-107">[RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) uygulayan çoğu kitaplık Microsoft Identity platformuna bağlanabilecektir.</span><span class="sxs-lookup"><span data-stu-id="59c61-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="59c61-108">Microsoft, 3 düzeltmelerin kitaplıkları taraf ve bu kitaplıkları gözden yapılmadı sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="59c61-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="59c61-109">Bu örnek, Azure AD B2C ile temel senaryolarda uyumluluk için test edilmiştir AppAuth adlı 3 bir taraf kitaplık kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="59c61-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="59c61-110">Kitaplığın açık kaynaklı proje yönlendirilmiş sorunları ve özellik istekleri.</span><span class="sxs-lookup"><span data-stu-id="59c61-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="59c61-111">Lütfen bakın [bu makalede](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="59c61-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="59c61-112">OAuth2 veya OpenID Connect kullanmaya yeni başladıysanız bu örnek yapılandırmanın büyük bölümü sizin için çok anlamlı olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="59c61-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="59c61-113">[burada belgelediğimiz protokolün genel bakışına](active-directory-b2c-reference-protocols.md) kısaca bakmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="59c61-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="59c61-114">Azure AD B2C dizini alma</span><span class="sxs-lookup"><span data-stu-id="59c61-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="59c61-115">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="59c61-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="59c61-116">Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="59c61-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="59c61-117">Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="59c61-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="59c61-118">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="59c61-118">Create an application</span></span>

<span data-ttu-id="59c61-119">Ardından B2C dizininizde uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="59c61-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="59c61-120">Bu, uygulamanız ile güvenli bir şekilde iletişim kurması için gereken bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="59c61-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="59c61-121">Mobil bir uygulama oluşturmak için izlemeniz [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="59c61-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="59c61-122">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="59c61-122">Be sure to:</span></span>

* <span data-ttu-id="59c61-123">Dahil bir **Native Client** uygulamadaki.</span><span class="sxs-lookup"><span data-stu-id="59c61-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="59c61-124">Uygulamanıza atanan **Uygulama Kimliği**'ni kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="59c61-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="59c61-125">Bu daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="59c61-125">You will need this later.</span></span>
* <span data-ttu-id="59c61-126">Bir yerel istemcisi ayarlama **yeniden yönlendirme URI'si** (örneğin com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="59c61-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="59c61-127">Buna da daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="59c61-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="59c61-128">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="59c61-128">Create your policies</span></span>

<span data-ttu-id="59c61-129">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="59c61-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="59c61-130">Bu uygulama bir kimlik deneyimi içerir: bir birleşik oturum açma ve kaydolma.</span><span class="sxs-lookup"><span data-stu-id="59c61-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="59c61-131">Bölümünde açıklandığı gibi bu ilkeyi oluşturmak gereken [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="59c61-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="59c61-132">İlkeyi oluştururken şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="59c61-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="59c61-133">Seçin **görünen adı** ilkenizde kaydolma özniteliği olarak.</span><span class="sxs-lookup"><span data-stu-id="59c61-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="59c61-134">Her ilkede uygulamanın talep ettiği **Görünen ad** ve **Nesne Kimliği** öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="59c61-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="59c61-135">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59c61-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="59c61-136">Oluşturduktan sonra her ilkenin **Adını** kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59c61-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="59c61-137">`b2c_1_` önekine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="59c61-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="59c61-138">Bu ilke adına daha sonra ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="59c61-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="59c61-139">İlkelerinizi oluşturduktan sonra uygulamanızı oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="59c61-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="59c61-140">Örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="59c61-140">Download the sample code</span></span>

<span data-ttu-id="59c61-141">Azure AD B2C ile AppAuth kullanan bir çalışma örneği sağladık [github'da](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="59c61-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="59c61-142">Kodu indirin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="59c61-142">You can download the code and run it.</span></span> <span data-ttu-id="59c61-143">Hızlı bir şekilde kendi Azure AD B2C Yapılandırması'ndaki yönergeleri izleyerek kullanılarak kendi uygulamanızı kullanmaya [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="59c61-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="59c61-144">Örnek tarafından sağlanan örnek bir değişikliktir [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="59c61-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="59c61-145">Lütfen AppAuth ve özellikleri hakkında daha fazla bilgi edinmek için kendi sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="59c61-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="59c61-146">Azure AD B2C ile AppAuth kullanmak için uygulamanızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="59c61-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="59c61-147">AppAuth destekleyen Android API 16 (Jellybean) ve üstü.</span><span class="sxs-lookup"><span data-stu-id="59c61-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="59c61-148">API 23 kullanmanızı öneririz ve üstü.</span><span class="sxs-lookup"><span data-stu-id="59c61-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="59c61-149">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="59c61-149">Configuration</span></span>

<span data-ttu-id="59c61-150">Azure AD B2C ile iletişim URI bulma belirterek veya yetkilendirme uç noktası ve belirteç uç noktası URI belirterek yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59c61-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="59c61-151">Her iki durumda da, aşağıdaki bilgiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="59c61-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="59c61-152">Kiracı kimliği (ör. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="59c61-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="59c61-153">İlke adı (örneğin B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="59c61-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="59c61-154">Yetkilendirme ve belirteç uç noktası URI otomatik olarak bulmayı seçerseniz, bulma URI bilgi fetch gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="59c61-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="59c61-155">Kiracı değiştirerek URI oluşturulabilir bulma\_kimliği ve ilke\_aşağıdaki URL adı:</span><span class="sxs-lookup"><span data-stu-id="59c61-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="59c61-156">Ardından, yetkilendirme ve belirteç uç noktası URI edinmeli ve aşağıdaki çalıştırarak AuthorizationServiceConfiguration nesneyi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="59c61-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="59c61-157">Yetkilendirme ve belirteç uç noktası URI elde etmek için bulma kullanmak yerine, ayrıca bunları açıkça Kiracı değiştirerek belirtebilirsiniz\_kimliği ve ilke\_adı URL'nin aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="59c61-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="59c61-158">AuthorizationServiceConfiguration nesnesi oluşturmak için aşağıdaki kodu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="59c61-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="59c61-159">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="59c61-159">Authorizing</span></span>

<span data-ttu-id="59c61-160">Yapılandırma veya bir yetkilendirme hizmet yapılandırmasını alma sonra bir yetkilendirme isteği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="59c61-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="59c61-161">İsteği oluşturmak için aşağıdaki bilgiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="59c61-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="59c61-162">İstemci kimliği (örneğin 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="59c61-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="59c61-163">Özel bir şema ile (örneğin com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect) yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="59c61-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="59c61-164">Olursa, her iki öğe kaydedildi [uygulamanızı kaydetme](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="59c61-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="59c61-165">Lütfen [AppAuth Kılavuzu](https://openid.github.io/AppAuth-Android/) işleminin geri kalanında tamamlamak hakkında.</span><span class="sxs-lookup"><span data-stu-id="59c61-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="59c61-166">Hızlı bir şekilde bir çalışma uygulaması ile çalışmaya başlamak ihtiyacınız varsa kullanıma [bizim örnek](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="59c61-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="59c61-167">Adımları [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) kendi Azure AD B2C yapılandırma girmek için.</span><span class="sxs-lookup"><span data-stu-id="59c61-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="59c61-168">Biz her zaman görüş ve öneriler için açık!</span><span class="sxs-lookup"><span data-stu-id="59c61-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="59c61-169">Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, sayfanın sonundaki görüşlerinize değer veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="59c61-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="59c61-170">Özellik istekleri için bunları Ekle [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="59c61-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

