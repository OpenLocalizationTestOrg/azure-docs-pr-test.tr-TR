---
title: "aaaAzure Active Directory v2.0 Android uygulaması | Microsoft Docs"
description: "Nasıl toobuild kişisel Microsoft hesabı ve iş veya Okul hesapları hem çağrıları kullanıcılar oturum açtığında bir Android uygulaması hello grafik API'si üçüncü taraf kitaplıklar kullanılarak."
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
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="58a98-103">Grafik API'si hello v2.0 uç kullanarak bir üçüncü taraf kitaplık kullanılarak oturum açma tooan Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="58a98-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="58a98-104">Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="58a98-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="58a98-105">Geliştiricilerin hizmetlerimizle ile toointegrate istedikleri herhangi bir kitaplığı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58a98-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="58a98-106">toohelp geliştiricilerin platformumuzu diğer kitaplıklarla birlikte kullanmak, biz bu bir toodemonstrate gibi birkaç izlenecek nasıl yazdıktan tooconfigure üçüncü taraf kitaplıklar tooconnect toohello Microsoft kimlik platformu.</span><span class="sxs-lookup"><span data-stu-id="58a98-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="58a98-107">Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) toohello Microsoft kimlik platformu bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="58a98-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="58a98-108">Bu izlenecek yol oluşturur hello uygulamasıyla kullanıcılar tootheir kuruluşta oturum ve ardından kendileri için kuruluşlarında hello grafik API'sini kullanarak arama.</span><span class="sxs-lookup"><span data-stu-id="58a98-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="58a98-109">Yeni tooOAuth2 veya Openıd Connect değilseniz, bu örnek yapılandırmanın çoğunu algılama tooyou oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="58a98-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="58a98-110">Okumanızı öneririz [2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md) arka planı için.</span><span class="sxs-lookup"><span data-stu-id="58a98-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="58a98-111">Merhaba OAuth2 veya Openıd Connect standartları, koşullu erişim ve Intune ilke yönetimi gibi bir ifadeye sahip bazı özellikleri, bizim açık kaynak Microsoft Azure kimlik kitaplıkları, toouse gerektirir.</span><span class="sxs-lookup"><span data-stu-id="58a98-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="58a98-112">Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="58a98-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="58a98-113">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="58a98-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="58a98-114">Github'dan Hello kodu indirme</span><span class="sxs-lookup"><span data-stu-id="58a98-114">Download hello code from GitHub</span></span>
<span data-ttu-id="58a98-115">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="58a98-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="58a98-116">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="58a98-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="58a98-117">Hello örnek ayrıca indirebilirsiniz ve hemen başlayın:</span><span class="sxs-lookup"><span data-stu-id="58a98-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="58a98-118">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="58a98-118">Register an app</span></span>
<span data-ttu-id="58a98-119">Merhaba yeni bir uygulama oluşturma [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya ayrıntılı adımları hello izleyin [nasıl tooregister hello v2.0 uç noktası ile uygulama](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="58a98-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="58a98-120">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="58a98-120">Make sure to:</span></span>

* <span data-ttu-id="58a98-121">Kopya hello **uygulama kimliği** , olduğundan atanan tooyour uygulama yakında gerekir.</span><span class="sxs-lookup"><span data-stu-id="58a98-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="58a98-122">Merhaba eklemek **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="58a98-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="58a98-123">Not: hello uygulama kayıt portalı sağlayan bir **yeniden yönlendirme URI'si** değeri.</span><span class="sxs-lookup"><span data-stu-id="58a98-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="58a98-124">Ancak, bu örnekte hello varsayılan değerini kullanmalısınız `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="58a98-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="58a98-125">Merhaba NXOAuth2 üçüncü taraf kitaplığını indirin ve çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58a98-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="58a98-126">Bu kılavuzda hello github'dan Google Openıd Connect kodunu hello üzerinde dayalı bir OAuth2 kitaplığı olan OIDCAndroidLib kullanır.</span><span class="sxs-lookup"><span data-stu-id="58a98-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="58a98-127">Merhaba yerel uygulama profilini uygular ve hello hello kullanıcı yetkilendirme uç noktasını destekler.</span><span class="sxs-lookup"><span data-stu-id="58a98-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="58a98-128">Bunlar hello Microsoft identity platformu ile toointegrate gerekir tüm hello noktalardır.</span><span class="sxs-lookup"><span data-stu-id="58a98-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="58a98-129">Merhaba OIDCAndroidLib depodaki tooyour bilgisayara kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="58a98-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="58a98-131">Android Studio ortamınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="58a98-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="58a98-132">Yeni bir Android Studio projesi oluşturun ve Başlangıç Sihirbazı'nda hello Varsayılanları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="58a98-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Android Studio'da yeni proje oluşturma](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Hedef Android cihazları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Bir etkinlik toomobile Ekle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="58a98-136">tooset klonlanmış hello depodaki toohello proje konumu proje modüllerinizi taşıyın.</span><span class="sxs-lookup"><span data-stu-id="58a98-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="58a98-137">Ayrıca hello projesi oluşturun ve toohello proje konumu doğrudan kopyalama.</span><span class="sxs-lookup"><span data-stu-id="58a98-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Proje modülleri](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="58a98-139">Merhaba proje modülleri ayarları hello bağlam menüsünü kullanarak veya hello Ctrl + Alt + Maj + S kısayolu kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="58a98-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Proje modülleri ayarları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="58a98-141">Merhaba proje kapsayıcı ayarları yalnızca istediğinden hello varsayılan uygulama modülünü Kaldır.</span><span class="sxs-lookup"><span data-stu-id="58a98-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![Merhaba varsayılan uygulama modülü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="58a98-143">Modülleri hello kopyalanan depodaki toohello geçerli projeden alın.</span><span class="sxs-lookup"><span data-stu-id="58a98-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="58a98-144">![İçeri aktarma gradle proje](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![yeni modül sayfa oluştur](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="58a98-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="58a98-145">Hello için bu adımları yineleyin `oidlib-sample` modülü.</span><span class="sxs-lookup"><span data-stu-id="58a98-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="58a98-146">Merhaba Hello oidclib bağımlılıkları denetleyin `oidlib-sample` modülü.</span><span class="sxs-lookup"><span data-stu-id="58a98-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![Merhaba oidlib örnek modül oidclib bağımlılıkları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="58a98-148">Tıklatın **Tamam** ve gradle eşitleme için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="58a98-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="58a98-149">Settings.gradle gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="58a98-149">Your settings.gradle should look like:</span></span>
   
    ![Settings.gradle ekran görüntüsü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="58a98-151">Merhaba örnek uygulama toomake emin yapı düzgün çalışmasını hello örneği.</span><span class="sxs-lookup"><span data-stu-id="58a98-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="58a98-152">Mümkün toouse bu Azure Active Directory ile henüz olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="58a98-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="58a98-153">Biz tooconfigure bazı uç noktaları ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="58a98-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="58a98-154">Merhaba örnek uygulaması özelleştirme başlamadan önce bir Android Studio sorunları yok tooensure budur.</span><span class="sxs-lookup"><span data-stu-id="58a98-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="58a98-155">Derleme ve çalıştırma `oidlib-sample` Android Studio'da hello hedefi olarak.</span><span class="sxs-lookup"><span data-stu-id="58a98-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Oidlib örnek yapı ilerlemesi](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="58a98-157">Merhaba silme `app ` Android Studio güvenliği silmez çünkü hello projeden hello modülü kaldırıldığında bırakıldı dizini.</span><span class="sxs-lookup"><span data-stu-id="58a98-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Merhaba uygulama dizini içeren dosya yapısı](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="58a98-159">Açık hello **yapılandırmalarını Düzenle** hello projeden hello modülü kaldırıldığında, ayrıca sol menü tooremove çalıştırmak hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="58a98-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="58a98-160">![Düzen yapılandırmaları menüsü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![uygulama yapılandırmasını çalıştırın](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="58a98-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="58a98-161">Merhaba örneğinin Hello uç noktalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="58a98-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="58a98-162">Merhaba sahip olduğunuza `oidlib-sample` başarıyla çalışırken, bazı uç noktaları tooget Azure Active Directory ile bu çalışma düzenleyelim.</span><span class="sxs-lookup"><span data-stu-id="58a98-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="58a98-163">Merhaba oidc_clientconf.xml dosyasını düzenleyerek istemcinizi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="58a98-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="58a98-164">OAuth2 akışları yalnızca tooget bir belirteç kullanarak ve hello grafik API'sini çağırmak için hello istemci toodo OAuth2 yalnızca ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="58a98-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="58a98-165">OIDC bir sonraki örnekte gelecektir.</span><span class="sxs-lookup"><span data-stu-id="58a98-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="58a98-166">Merhaba kayıt Portalı'ndan alınan istemci Kimliğiniz yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="58a98-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="58a98-167">Aşağıda, yeniden yönlendirme URI'si hello biri ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="58a98-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="58a98-168">Grafik API'si sipariş tooaccess hello, kapsamı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="58a98-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="58a98-169">Merhaba `User.Read` değeri `oidc_scopes` , tooread hello temel profil hello imzalı kullanıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="58a98-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="58a98-170">Tüm hello kullanılabilir kapsamların hakkında daha fazla bilgiyi [Microsoft Graph izin kapsamları](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="58a98-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="58a98-171">İlgili açıklamalar istiyorsanız `openid` veya `offline_access` kapsamlarda Openıd Connect, bkz: [2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="58a98-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="58a98-172">Merhaba oidc_endpoints.xml dosyasını düzenleyerek, istemci uç noktalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="58a98-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="58a98-173">Açık hello `oidc_endpoints.xml` dosya ve hello aşağıdaki değişiklikler yapın:</span><span class="sxs-lookup"><span data-stu-id="58a98-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="58a98-174">OAuth2, protokol olarak kullanıyorsanız, bu uç noktaları asla değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58a98-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="58a98-175">Merhaba uç noktaları için `userInfoEndpoint` ve `revocationEndpoint` şu anda Azure Active Directory tarafından desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="58a98-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="58a98-176">Bunlar hello varsayılan example.com değerle bırakırsanız, hello örnek kullanılabilir olmadıklarını :-) uyarılmak</span><span class="sxs-lookup"><span data-stu-id="58a98-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="58a98-177">Bir grafik API çağrısı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="58a98-177">Configure a Graph API call</span></span>
* <span data-ttu-id="58a98-178">Açık hello `HomeActivity.java` dosya ve hello aşağıdaki değişiklikler yapın:</span><span class="sxs-lookup"><span data-stu-id="58a98-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="58a98-179">Burada basit bir grafik API çağrısı bizim bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="58a98-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="58a98-180">Toodo gereken tüm hello değişiklik izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="58a98-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="58a98-181">Merhaba çalıştırmak `oidlib-sample` uygulama ve tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="58a98-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="58a98-182">Başarıyla kimlik doğruladınız sonra hello seçin **korumalı kaynak isteği** tootest, çağrı toohello grafik API'si düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58a98-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="58a98-183">Ürünümüz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="58a98-183">Get security updates for our product</span></span>
<span data-ttu-id="58a98-184">Güvenlik olayları hakkında tooget bildirimler hello ziyaret ederek öneririz [güvenlik TechCenter](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="58a98-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

