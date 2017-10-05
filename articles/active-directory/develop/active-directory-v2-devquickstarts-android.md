---
title: "Azure Active Directory v2.0 Android uygulaması | Microsoft Docs"
description: "Kullanıcıların kişisel bir Microsoft hesabı ve iş veya Okul hesapları hem çağrıları grafik API'si ile üçüncü taraf kitaplıklarını kullanarak oturum açtığında bir Android uygulaması oluşturma."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="27005-103">Grafik API'si v2.0 uç noktası kullanarak bir üçüncü taraf kitaplık kullanılarak bir Android uygulaması için oturum açma ekleme</span><span class="sxs-lookup"><span data-stu-id="27005-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="27005-104">Microsoft kimlik platformu OAuth2 ve OpenID Connect gibi açık standartlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="27005-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="27005-105">Geliştiricilerin hizmetlerimizle tümleştirmek istediği herhangi bir kitaplığı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27005-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="27005-106">Geliştiricilerin platformumuzu diğer kitaplıklarla birlikte kullanmak için Microsoft identity platformuna bağlanmak için üçüncü taraf kitaplıklarını yapılandırmak nasıl göstermek için bunun gibi birkaç izlenecek yazdıktan.</span><span class="sxs-lookup"><span data-stu-id="27005-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="27005-107">Uygulayan çoğu kitaplık [RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) Microsoft identity platformuna bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="27005-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="27005-108">Bu izlenecek yol oluşturur uygulamasıyla kullanıcılar kendi kuruluşa oturum açabilir ve ardından kendileri için kuruluşlarında grafik API'sini kullanarak arama.</span><span class="sxs-lookup"><span data-stu-id="27005-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="27005-109">OAuth2 veya Openıd Connect kullanmaya yeni başladıysanız Bu örnek yapılandırmanın çoğunu sizin için anlamlı değil.</span><span class="sxs-lookup"><span data-stu-id="27005-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="27005-110">Okumanızı öneririz [2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md) arka planı için.</span><span class="sxs-lookup"><span data-stu-id="27005-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="27005-111">Bir ifade koşullu erişim ve Intune ilke yönetimi gibi OAuth2 veya Openıd Connect standartları olan bazı özellikleri, bizim açık kaynak Microsoft Azure kimlik kitaplıkları kullanmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="27005-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="27005-112">V2.0 uç noktası, tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="27005-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="27005-113">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="27005-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="27005-114">Github'dan kodu indirme</span><span class="sxs-lookup"><span data-stu-id="27005-114">Download the code from GitHub</span></span>
<span data-ttu-id="27005-115">Bu öğretici için kod [GitHub'da](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2) korunur.</span><span class="sxs-lookup"><span data-stu-id="27005-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="27005-116">İzlemek için [uygulamanın çatısını bir .zip karşıdan](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="27005-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="27005-117">Örnek ayrıca indirebilirsiniz ve hemen başlayın:</span><span class="sxs-lookup"><span data-stu-id="27005-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="27005-118">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="27005-118">Register an app</span></span>
<span data-ttu-id="27005-119">En yeni bir uygulama oluşturma [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya ayrıntılı adımları izleyin [v2.0 uç noktası ile bir uygulama nasıl](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="27005-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="27005-120">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="27005-120">Make sure to:</span></span>

* <span data-ttu-id="27005-121">Kopya **uygulama kimliği** atanan uygulamanıza yakında gerekir çünkü.</span><span class="sxs-lookup"><span data-stu-id="27005-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="27005-122">Ekleme **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="27005-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="27005-123">Not: Uygulama kayıt Portalı'nı sağlayan bir **yeniden yönlendirme URI'si** değeri.</span><span class="sxs-lookup"><span data-stu-id="27005-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="27005-124">Ancak, bu örnekte, varsayılan değeri kullanmalıdır `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="27005-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="27005-125">NXOAuth2 üçüncü taraf kitaplığını indirin ve çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="27005-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="27005-126">Bu kılavuz için github'dan Google Openıd Connect kod ile temel bir OAuth2 kitaplığı olan OIDCAndroidLib kullanır.</span><span class="sxs-lookup"><span data-stu-id="27005-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="27005-127">Yerel uygulama profilini uygular ve kullanıcı yetkilendirme uç noktası destekler.</span><span class="sxs-lookup"><span data-stu-id="27005-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="27005-128">Microsoft kimlik platformu ile tümleştirme için gereken her şeyi bunlar.</span><span class="sxs-lookup"><span data-stu-id="27005-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="27005-129">Bilgisayarınıza OIDCAndroidLib depoyu kopyalama.</span><span class="sxs-lookup"><span data-stu-id="27005-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="27005-131">Android Studio ortamınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="27005-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="27005-132">Yeni bir Android Studio projesi oluşturun ve Sihirbazı'nda varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="27005-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Android Studio'da yeni proje oluşturma](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Hedef Android cihazları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Mobil bir etkinlik ekleme](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="27005-136">Proje modüllerinizi ayarlamak için proje konumuna kopyalanan depoyu taşıyın.</span><span class="sxs-lookup"><span data-stu-id="27005-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="27005-137">Ayrıca projesi oluşturun ve doğrudan proje konumuna kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="27005-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Proje modülleri](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="27005-139">Proje modülleri ayarları bağlam menüsünü kullanarak veya Ctrl + Alt + Maj + S kısayol kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="27005-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Proje modülleri ayarları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="27005-141">Proje kapsayıcı ayarları yalnızca istediğinden varsayılan uygulama modülünü Kaldır.</span><span class="sxs-lookup"><span data-stu-id="27005-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![Varsayılan uygulama modülü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="27005-143">Modülleri geçerli projeye kopyalanan deposuna alın.</span><span class="sxs-lookup"><span data-stu-id="27005-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="27005-144">![İçeri aktarma gradle proje](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![yeni modül sayfa oluştur](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="27005-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="27005-145">İçin bu adımları yineleyin `oidlib-sample` modülü.</span><span class="sxs-lookup"><span data-stu-id="27005-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="27005-146">Oidclib bağımlılıkları denetleme `oidlib-sample` modülü.</span><span class="sxs-lookup"><span data-stu-id="27005-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![oidlib örnek modül oidclib bağımlılıkları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="27005-148">Tıklatın **Tamam** ve gradle eşitleme için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="27005-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="27005-149">Settings.gradle gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="27005-149">Your settings.gradle should look like:</span></span>
   
    ![Settings.gradle ekran görüntüsü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="27005-151">Emin olmak için örnek uygulaması derleme düzgün çalışmasını örnek.</span><span class="sxs-lookup"><span data-stu-id="27005-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="27005-152">Bu Azure Active Directory ile henüz kullanmanız mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="27005-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="27005-153">Bazı uç noktaları öncelikle yapılandırmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="27005-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="27005-154">Bu örnek uygulama özelleştirme başlamadan önce bir Android Studio sorunları yok sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="27005-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="27005-155">Derleme ve çalıştırma `oidlib-sample` Android Studio'da hedefi olarak.</span><span class="sxs-lookup"><span data-stu-id="27005-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Oidlib örnek yapı ilerlemesi](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="27005-157">Silme `app ` Android Studio güvenliği silmez çünkü projeden modülü kaldırıldığında bırakıldı dizini.</span><span class="sxs-lookup"><span data-stu-id="27005-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Uygulama dizinindeki içeren dosya yapısı](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="27005-159">Açık **yapılandırmalarını Düzenle** projeden modülü kaldırıldığında, aynı zamanda sol çalıştırma yapılandırmasını kaldırmak üzere menüsü.</span><span class="sxs-lookup"><span data-stu-id="27005-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="27005-160">![Düzen yapılandırmaları menüsü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![uygulama yapılandırmasını çalıştırın](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="27005-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="27005-161">Örnek uç noktalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27005-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="27005-162">Sahip olduğunuza `oidlib-sample` başarıyla çalışırken, Azure Active Directory ile bu çalışma almak için bazı uç noktaları düzenleyelim.</span><span class="sxs-lookup"><span data-stu-id="27005-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="27005-163">Oidc_clientconf.xml dosyasını düzenleyerek istemcinizi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="27005-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="27005-164">Yalnızca bir belirteç almak ve grafik API'sini çağırmak için OAuth2 akışları kullandığınızdan, OAuth2 yalnızca yapmak için istemcinin ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="27005-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="27005-165">OIDC bir sonraki örnekte gelecektir.</span><span class="sxs-lookup"><span data-stu-id="27005-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="27005-166">Kayıt Portalı'ndan alınan istemci Kimliğiniz yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27005-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="27005-167">Yeniden yönlendirme URI'sine sahip bir aşağıdaki yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27005-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="27005-168">Grafik API'sine erişmek için gereken, kapsamı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27005-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="27005-169">`User.Read` Değeri `oidc_scopes` , kullanıcının temel profil imzalı okumanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="27005-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="27005-170">Kullanılabilir tüm kapsamların hakkında daha fazla bilgiyi [Microsoft Graph izin kapsamları](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="27005-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="27005-171">İlgili açıklamalar istiyorsanız `openid` veya `offline_access` kapsamlarda Openıd Connect, bkz: [2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="27005-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="27005-172">Oidc_endpoints.xml dosyasını düzenleyerek, istemci uç noktalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27005-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="27005-173">Açık `oidc_endpoints.xml` dosya ve aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="27005-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="27005-174">OAuth2, protokol olarak kullanıyorsanız, bu uç noktaları asla değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="27005-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="27005-175">Uç noktaları için `userInfoEndpoint` ve `revocationEndpoint` şu anda Azure Active Directory tarafından desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="27005-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="27005-176">Bu varsayılan example.com değerle bırakırsanız, örnekte kullanılabilir olmadıklarını :-) uyarılmak</span><span class="sxs-lookup"><span data-stu-id="27005-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="27005-177">Bir grafik API çağrısı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27005-177">Configure a Graph API call</span></span>
* <span data-ttu-id="27005-178">Açık `HomeActivity.java` dosya ve aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="27005-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="27005-179">Burada basit bir grafik API çağrısı bizim bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="27005-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="27005-180">Yapmanız gereken tüm değişiklikleri izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="27005-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="27005-181">Çalıştırma `oidlib-sample` uygulama ve tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="27005-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="27005-182">Başarıyla kimlik doğruladınız sonra seçin **korumalı kaynak isteği** aramanız grafik API'si için test etmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="27005-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="27005-183">Ürünümüz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="27005-183">Get security updates for our product</span></span>
<span data-ttu-id="27005-184">Ziyaret ederek güvenlik olayları hakkında bildirimleri almanızı öneririz [güvenlik TechCenter](https://technet.microsoft.com/security/dd252948) ve güvenlik önerisi uyarılarına abone.</span><span class="sxs-lookup"><span data-stu-id="27005-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

