---
title: "Azure Active Directory B2C: bir Android uygulamasını kullanarak bir belirteç alınırken | Microsoft Docs"
description: "Bu makale size nasıl gösterir toocreate, Azure Active Directory B2C toomanage kullanıcı kimliklerle AppAuth kullanır ve kullanıcıların kimliklerini bir Android uygulaması."
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
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="a2165-103">Azure AD B2C: Bir Android uygulamasını kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="a2165-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="a2165-104">Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2165-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="a2165-105">Böylece geliştiriciler tooleverage hizmetlerimizle ile toointegrate istedikleri herhangi bir kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="a2165-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="a2165-106">platformumuzu diğer kitaplıklarla birlikte kullanarak tooaid geliştiriciler, yazılan bu bir toodemonstrate gibi birkaç izlenecek nasıl tooconfigure 3 taraf kitaplıklar tooconnect toohello Microsoft kimlik platformu.</span><span class="sxs-lookup"><span data-stu-id="a2165-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="a2165-107">Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) mümkün tooconnect toohello Microsoft Identity platform olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2165-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="a2165-108">Microsoft, 3 düzeltmelerin kitaplıkları taraf ve bu kitaplıkları gözden yapılmadı sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="a2165-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="a2165-109">Bu örnek temel senaryolarda hello Azure AD B2C ile uyumluluk için test edilmiştir AppAuth adlı 3 bir taraf kitaplık kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="a2165-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="a2165-110">Sorunları ve özellik istekleri yönlendirilmiş toohello kitaplığın açık kaynaklı proje olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2165-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="a2165-111">Lütfen bakın [bu makalede](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a2165-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="a2165-112">Yeni tooOAuth2 veya Openıd Connect değilseniz bu örnek yapılandırmanın çoğunu kadar algılama tooyou oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a2165-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="a2165-113">Kısaca öneririz [biz burada belgelediğimiz hello protokolüne genel bakış](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a2165-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="a2165-114">Azure AD B2C dizini alma</span><span class="sxs-lookup"><span data-stu-id="a2165-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="a2165-115">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2165-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="a2165-116">Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a2165-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="a2165-117">Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a2165-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="a2165-118">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2165-118">Create an application</span></span>

<span data-ttu-id="a2165-119">Ardından B2C dizininizde uygulama toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2165-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="a2165-120">Bu, uygulamanız ile güvenli toocommunicate gereken bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="a2165-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="a2165-121">bir mobil uygulama toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a2165-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="a2165-122">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="a2165-122">Be sure to:</span></span>

* <span data-ttu-id="a2165-123">Dahil bir **Native Client** hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="a2165-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="a2165-124">Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="a2165-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="a2165-125">Bu daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="a2165-125">You will need this later.</span></span>
* <span data-ttu-id="a2165-126">Bir yerel istemcisi ayarlama **yeniden yönlendirme URI'si** (örneğin com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="a2165-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="a2165-127">Buna da daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="a2165-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="a2165-128">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2165-128">Create your policies</span></span>

<span data-ttu-id="a2165-129">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a2165-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a2165-130">Bu uygulama bir kimlik deneyimi içerir: bir birleşik oturum açma ve kaydolma.</span><span class="sxs-lookup"><span data-stu-id="a2165-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="a2165-131">Toocreate açıklandığı gibi bu ilkeyi gereken [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="a2165-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="a2165-132">Hello ilkesi oluşturduğunuzda, emin olun:</span><span class="sxs-lookup"><span data-stu-id="a2165-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="a2165-133">Merhaba seçin **görünen adı** ilkenizde kaydolma özniteliği olarak.</span><span class="sxs-lookup"><span data-stu-id="a2165-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="a2165-134">Merhaba seçin **görünen adı** ve **nesne kimliği** her ilkede uygulamanın talep.</span><span class="sxs-lookup"><span data-stu-id="a2165-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="a2165-135">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2165-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="a2165-136">Kopya hello **adı** oluşturduktan sonra her ilkenin.</span><span class="sxs-lookup"><span data-stu-id="a2165-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="a2165-137">Merhaba önekine sahip olmalıdır `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="a2165-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="a2165-138">Hello ilkesi adı daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="a2165-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="a2165-139">İlkelerinizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="a2165-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="a2165-140">Merhaba örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="a2165-140">Download hello sample code</span></span>

<span data-ttu-id="a2165-141">Azure AD B2C ile AppAuth kullanan bir çalışma örneği sağladık [github'da](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="a2165-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="a2165-142">Merhaba kodu indirin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2165-142">You can download hello code and run it.</span></span> <span data-ttu-id="a2165-143">Hızlı bir şekilde hello hello yönergeleri takip ederek kendi Azure AD B2C Yapılandırması'nı kullanarak kendi uygulamanızı kullanmaya [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="a2165-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="a2165-144">Merhaba örnektir tarafından sağlanan hello örnek değiştirilmesini [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="a2165-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="a2165-145">Lütfen AppAuth ve özellikleri hakkında daha fazla kendi sayfa toolearn adresini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="a2165-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="a2165-146">Uygulama toouse Azure AD B2C AppAuth ile değiştirme</span><span class="sxs-lookup"><span data-stu-id="a2165-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="a2165-147">AppAuth destekleyen Android API 16 (Jellybean) ve üstü.</span><span class="sxs-lookup"><span data-stu-id="a2165-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="a2165-148">API 23 kullanmanızı öneririz ve üstü.</span><span class="sxs-lookup"><span data-stu-id="a2165-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="a2165-149">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a2165-149">Configuration</span></span>

<span data-ttu-id="a2165-150">Azure AD B2C ile iletişim belirtme ya da hello bulma URI veya hello yetkilendirme uç noktası ve belirteç uç noktası URI belirterek yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2165-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="a2165-151">Her iki durumda da, aşağıdaki bilgilerle hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2165-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="a2165-152">Kiracı kimliği (ör. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="a2165-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="a2165-153">İlke adı (örneğin B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="a2165-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="a2165-154">Seçtiğiniz varsa tooautomatically hello yetkilendirme ve belirteç uç noktası URI bulmak, hello keşfi URI toofetch bilgilere ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2165-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="a2165-155">URI hello Kiracı değiştirerek oluşturulabilir hello bulma\_kimliği ve hello İlkesi\_URL aşağıdaki hello adı:</span><span class="sxs-lookup"><span data-stu-id="a2165-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="a2165-156">Ardından, hello yetkilendirme ve belirteç uç noktası URI edinmeli ve hello aşağıdakini çalıştırarak bir AuthorizationServiceConfiguration nesnesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a2165-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

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
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="a2165-157">Bulma tooobtain hello yetkilendirme ve belirteç uç noktası URI kullanmak yerine, ayrıca bunları açıkça hello Kiracı değiştirerek belirtebilirsiniz\_kimliği ve hello İlkesi\_adlarında hello URL'SİNİN aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="a2165-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="a2165-158">Aşağıdaki kod toocreate hello AuthorizationServiceConfiguration nesnenizin çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a2165-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="a2165-159">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="a2165-159">Authorizing</span></span>

<span data-ttu-id="a2165-160">Yapılandırma veya bir yetkilendirme hizmet yapılandırmasını alma sonra bir yetkilendirme isteği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="a2165-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="a2165-161">toocreate hello istek bilgisinden hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2165-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="a2165-162">İstemci kimliği (örneğin 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="a2165-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="a2165-163">Özel bir şema ile (örneğin com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect) yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="a2165-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="a2165-164">Olursa, her iki öğe kaydedildi [uygulamanızı kaydetme](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="a2165-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="a2165-165">Lütfen toohello bakın [AppAuth Kılavuzu](https://openid.github.io/AppAuth-Android/) nasıl toocomplete hello hello işleminin geri kalanında üzerinde.</span><span class="sxs-lookup"><span data-stu-id="a2165-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="a2165-166">Tooquickly gerekiyorsa bir çalışma uygulaması ile çalışmaya başlama, kullanıma [bizim örnek](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="a2165-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="a2165-167">Merhaba Hello adımları [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter kendi Azure AD B2C yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="a2165-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="a2165-168">Her zaman açık toofeedback ve öneriler duyuyoruz!</span><span class="sxs-lookup"><span data-stu-id="a2165-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="a2165-169">Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, hello sayfanın hello sonundaki görüşlerinize değer veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="a2165-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="a2165-170">Özellik istekleri için çok eklemediğiniz[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="a2165-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

