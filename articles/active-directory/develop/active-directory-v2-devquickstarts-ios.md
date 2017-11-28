---
title: "aaaAdd oturum açma tooan iOS uygulaması kullanarak Azure AD v2.0 uç hello | Microsoft Docs"
description: "Nasıl toobuild bir iOS uygulaması, kullanıcıların hem kişisel Microsoft hesabı ile ve iş veya Okul hesapları üçüncü taraf kitaplıklar kullanılarak imzalar."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="4f4db-103">Grafik API'si hello v2.0 uç kullanarak bir üçüncü taraf kitaplık kullanılarak oturum açma tooan iOS uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="4f4db-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="4f4db-104">Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="4f4db-105">Geliştiricilerin hizmetlerimizle ile toointegrate istedikleri herhangi bir kitaplığı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f4db-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="4f4db-106">toohelp geliştiricilerin platformumuzu diğer kitaplıklarla birlikte kullanmak, biz bu bir toodemonstrate gibi birkaç izlenecek nasıl yazdıktan tooconfigure üçüncü taraf kitaplıklar tooconnect toohello Microsoft kimlik platformu.</span><span class="sxs-lookup"><span data-stu-id="4f4db-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="4f4db-107">Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) toohello Microsoft kimlik platformu bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="4f4db-108">Bu izlenecek yol oluşturur hello uygulamasıyla kullanıcılar tootheir kuruluşunuzda oturum ve ardından başkaları için kuruluşlarında hello grafik API'sini kullanarak arama.</span><span class="sxs-lookup"><span data-stu-id="4f4db-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="4f4db-109">Yeni tooOAuth2 veya Openıd Connect değilseniz, bu örnek yapılandırmanın çoğunu algılama tooyou oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="4f4db-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="4f4db-110">Okumanızı öneririz [v2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md) arka planı için.</span><span class="sxs-lookup"><span data-stu-id="4f4db-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="4f4db-111">Merhaba OAuth2 veya Openıd Connect standartları, koşullu erişim ve Intune ilke yönetimi gibi bir ifadeye sahip bazı özellikleri, bizim açık kaynak Microsoft Azure kimlik kitaplıkları, toouse gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="4f4db-112">Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4f4db-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="4f4db-113">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4f4db-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="4f4db-114">Github'dan kodu indirme</span><span class="sxs-lookup"><span data-stu-id="4f4db-114">Download code from GitHub</span></span>
<span data-ttu-id="4f4db-115">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="4f4db-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="4f4db-116">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="4f4db-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="4f4db-117">Hello örnek ayrıca indirebilirsiniz ve hemen başlayın:</span><span class="sxs-lookup"><span data-stu-id="4f4db-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="4f4db-118">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="4f4db-118">Register an app</span></span>
<span data-ttu-id="4f4db-119">Merhaba yeni bir uygulama oluşturma [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya ayrıntılı adımları hello izleyin [nasıl tooregister hello v2.0 uç noktası ile uygulama](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4f4db-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="4f4db-120">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="4f4db-120">Make sure to:</span></span>

* <span data-ttu-id="4f4db-121">Kopya hello **uygulama kimliği** , olduğundan atanan tooyour uygulama yakında gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="4f4db-122">Merhaba eklemek **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="4f4db-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="4f4db-123">Kopya hello **yeniden yönlendirme URI'si** hello portalından.</span><span class="sxs-lookup"><span data-stu-id="4f4db-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="4f4db-124">Merhaba varsayılan değeri kullanın `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4f4db-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="4f4db-125">Merhaba üçüncü taraf NXOAuth2 kitaplık indirmeniz ve çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f4db-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="4f4db-126">Bu kılavuz için github'dan Mac OS X ve iOS (Cocoa ve Cocoa touch) için bir OAuth2 kitaplığı olan OAuth2Client hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="4f4db-127">Bu kitaplık hello OAuth2 belirtimi taslak 10 temel alır. Merhaba yerel uygulama profilini uygular ve hello hello kullanıcı yetkilendirme uç noktasını destekler.</span><span class="sxs-lookup"><span data-stu-id="4f4db-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="4f4db-128">Bunlar hello Microsoft identity platformu ile toointegrate gerekir tüm hello noktalardır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="4f4db-129">CocoaPods kullanarak Hello kitaplığı tooyour projesi ekleyin</span><span class="sxs-lookup"><span data-stu-id="4f4db-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="4f4db-130">CocoaPods, Xcode projeleri için bir bağımlılık yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="4f4db-131">Merhaba önceki yükleme adımlarını otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="4f4db-132">Toothis podfile aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4f4db-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="4f4db-133">CocoaPods kullanarak Hello podfile dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="4f4db-134">Bu, yükleyeceğiniz yeni bir Xcode çalışma alanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f4db-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="4f4db-135">Merhaba projenin Hello yapısı keşfedin</span><span class="sxs-lookup"><span data-stu-id="4f4db-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="4f4db-136">Yapı izlenerek hello hello çatıyı bizim proje için kurun:</span><span class="sxs-lookup"><span data-stu-id="4f4db-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="4f4db-137">UPN arama ile ana görünüm</span><span class="sxs-lookup"><span data-stu-id="4f4db-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="4f4db-138">Merhaba veriler için ayrıntılı görünüm hello seçili kullanıcı hakkında</span><span class="sxs-lookup"><span data-stu-id="4f4db-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="4f4db-139">Bir oturum açma kullanıcı toohello uygulama tooquery hello grafiğinde burada oturum görünümü</span><span class="sxs-lookup"><span data-stu-id="4f4db-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="4f4db-140">Biz hello iskelet tooadd kimlik doğrulaması toovarious dosyalarında taşınır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="4f4db-141">Diğer bölümleri hello görsel kod gibi hello kod tooidentity ilgilidir değil ancak sizin için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="4f4db-142">Merhaba Kitaplığı'nda hello settings.plst dosya ayarlama</span><span class="sxs-lookup"><span data-stu-id="4f4db-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="4f4db-143">Merhaba Hello hızlı başlangıç projesi açmak `settings.plist` dosya.</span><span class="sxs-lookup"><span data-stu-id="4f4db-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="4f4db-144">Hello Azure portal kullanılan hello bölüm tooreflect hello değerleri hello öğelerinde Hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="4f4db-145">Merhaba Active Directory kimlik doğrulama kitaplığı kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="4f4db-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="4f4db-146">Merhaba `clientId` hello portalından kopyalandığından, uygulamanızın hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="4f4db-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="4f4db-147">Merhaba `redirectUri` hello yeniden yönlendirme URL'si sağlanan bu hello portalıdır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="4f4db-148">Merhaba, LoginViewController içinde NXOAuth2Client kitaplığınızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4f4db-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="4f4db-149">Merhaba NXOAuth2Client kitaplığınızı ayarlayın bazı değerler tooget gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="4f4db-150">Bu görev tamamlandıktan sonra hello alınan belirteç toocall hello grafik API'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f4db-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="4f4db-151">Çünkü `LoginView` dilediğiniz zaman çağrılacağı tooauthenticate ihtiyacımız, tooput yapılandırma değerlerini toothat dosyasında mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="4f4db-152">Bazı değerler toohello ekleyelim `LoginViewController.m` kimlik doğrulama ve yetkilendirme için dosya tooset hello bağlamı.</span><span class="sxs-lookup"><span data-stu-id="4f4db-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="4f4db-153">Merhaba değerleri ayrıntılarını hello kod izleyin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-153">Details about hello values follow hello code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="4f4db-154">Merhaba kod ayrıntılarını bakalım.</span><span class="sxs-lookup"><span data-stu-id="4f4db-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="4f4db-155">Merhaba ilk dizesi içindir `scopes`.</span><span class="sxs-lookup"><span data-stu-id="4f4db-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="4f4db-156">Merhaba `User.Read` değeri tooread hello temel profilini kullanıcı imzalı hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f4db-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="4f4db-157">Tüm hello kullanılabilir kapsamların hakkında daha fazla bilgiyi [Microsoft Graph izin kapsamları](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="4f4db-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="4f4db-158">İçin `authURL`, `loginURL`, `bhh`, ve `tokenURL`, daha önce sağlanan hello değerleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="4f4db-159">Merhaba açık kaynak Microsoft Azure kimlik kitaplıklarını kullanırsanız, size bu verileri sizin için bizim meta veri uç noktasının kullanarak çekme.</span><span class="sxs-lookup"><span data-stu-id="4f4db-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="4f4db-160">Biz bu değerleri sizin yerinize ayıklamak hello sabit iş yaptık.</span><span class="sxs-lookup"><span data-stu-id="4f4db-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="4f4db-161">Merhaba `keychain` değerdir NXOAuth2Client kitaplığının hello hello kapsayıcı toocreate Anahtarlık toostore belirteçlerinizi kullanır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="4f4db-162">Belirleyebileceğiniz tooget çoklu oturum açma (SSO) çok sayıda uygulamada istiyorsanız, hello uygulamalarınızın her birinde aynı Anahtarlıkta ve istek hello kullanılmasını Xcode yetkilendirmeler içinde.</span><span class="sxs-lookup"><span data-stu-id="4f4db-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="4f4db-163">Bu hello Apple belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="4f4db-164">Bu değerlerin Hello rest gerekli toouse hello kitaplıkta ve toocarry değerleri toohello bağlamı yerler oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="4f4db-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="4f4db-165">Bir URL önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f4db-165">Create a URL cache</span></span>
<span data-ttu-id="4f4db-166">İçinde `(void)viewDidLoad()`, her zaman adlandırılan hello görünüm yüklendikten sonra hello aşağıdaki kodu primes bizim kullanmak için bir önbellek.</span><span class="sxs-lookup"><span data-stu-id="4f4db-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="4f4db-167">Hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4f4db-167">Add hello following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="4f4db-168">Oturum açma için bir Web görünümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f4db-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="4f4db-169">Bir Web görünümü hello kullanıcıdan SMS metin iletisi (yapılandırılmışsa) gibi ek faktörler veya hata iletilerini toohello kullanıcıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="4f4db-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="4f4db-170">Burada, hello WebView ve daha sonra yazma hello yedekleme olacağını kod toohandle hello geri aramalar hello WebView hello kimlik Hizmetleri'nden ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="4f4db-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="4f4db-171">Merhaba WebView yöntemlerini toohandle kimlik doğrulama geçersiz kıl</span><span class="sxs-lookup"><span data-stu-id="4f4db-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="4f4db-172">tootell hello daha önce anlatıldığı gibi bir kullanıcı olarak toosign gerektiğinde ne olacağını WebView, koddan hello yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f4db-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="4f4db-173">Kod toohandle hello hello OAuth2 isteğinin sonucunu yazma</span><span class="sxs-lookup"><span data-stu-id="4f4db-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="4f4db-174">Merhaba aşağıdaki kodu WebView hello döndürür hello Redirecturl'yi işleyecek.</span><span class="sxs-lookup"><span data-stu-id="4f4db-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="4f4db-175">Kimlik doğrulaması başarısız olmadıysa hello kodu yeniden deneyecek.</span><span class="sxs-lookup"><span data-stu-id="4f4db-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="4f4db-176">Bu sırada, hello kitaplığı hello konsolda görebileceğiniz veya zaman uyumsuz olarak işlemek hello hata sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f4db-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="4f4db-177">OAuth (hesap deposu olarak adlandırılır) bağlam Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4f4db-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="4f4db-178">Burada çağırabilirsiniz `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` hello paylaşılan hesap deposu hello uygulama toobe mümkün tooaccess istediğiniz her hizmet için.</span><span class="sxs-lookup"><span data-stu-id="4f4db-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="4f4db-179">Merhaba hesap türü için belirli bir hizmeti bir tanımlayıcı olarak kullanılan bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="4f4db-180">Hello grafik API'si eriştiğiniz çünkü hello kod olarak tooit başvuruyor `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="4f4db-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="4f4db-181">Ardından herhangi bir şey hello belirteciyle değiştirildiğinde bildirir bir gözlemci ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="4f4db-182">Merhaba belirteci aldıktan sonra hello kullanıcı geri toohello iade `masterView`.</span><span class="sxs-lookup"><span data-stu-id="4f4db-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="4f4db-183">Ana görünüm toosearch Hello ayarlayın ve hello grafik API'si hello kullanıcıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="4f4db-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="4f4db-184">Döndürülen veriler hello kılavuzunda hello görüntüleyen bir ana-View-Controller (MVC) uygulama hello bu kılavuz kapsamında değildir ve birçok çevrimiçi eğitim açıklama nasıl toobuild biri.</span><span class="sxs-lookup"><span data-stu-id="4f4db-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="4f4db-185">Bu kod hello iskelet dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="4f4db-186">Ancak, bu MVC uygulamasındaki birkaç şey ile toodeal gerekir:</span><span class="sxs-lookup"><span data-stu-id="4f4db-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="4f4db-187">Bir kullanıcı bir şey hello arama alanına yazdığında müdahale</span><span class="sxs-lookup"><span data-stu-id="4f4db-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="4f4db-188">Bir nesneyi veri arka toohello MasterView hello kılavuzunda hello sonuçları görüntüleyebilmesi sağlayın</span><span class="sxs-lookup"><span data-stu-id="4f4db-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="4f4db-189">Biz bu aşağıdaki gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f4db-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="4f4db-190">Oturum açtınız varsa onay toosee ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="4f4db-191">Merhaba kullanıcı, imzalı değilse zaten varsa bir simge hello önbelleğinde akıllı toocheck olacak şekilde hello uygulama az yapar.</span><span class="sxs-lookup"><span data-stu-id="4f4db-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="4f4db-192">Toohello LoginView hello kullanıcı toosign için yönlendirme değil, varsa.</span><span class="sxs-lookup"><span data-stu-id="4f4db-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="4f4db-193">Geri çağırma bir görünüm yüklenirken hello en iyi şekilde toodo eylemler varsa, toouse hello `viewDidLoad()` Apple bize sağlayan yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="4f4db-194">Güncelleştirme hello tablo veri alındığında görünümü</span><span class="sxs-lookup"><span data-stu-id="4f4db-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="4f4db-195">Merhaba grafik API'si veri döndürdüğünde toodisplay hello veri gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="4f4db-196">Kolaylık olması için burada tüm hello kodu tooupdate hello tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="4f4db-197">MVC Demirbaş kodunuzda hello doğru değerleri yalnızca yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f4db-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="4f4db-198">Birisi hello arama alanına yazdığında bir şekilde toocall hello grafik API'si sağlayın</span><span class="sxs-lookup"><span data-stu-id="4f4db-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="4f4db-199">Bir kullanıcı hello kutusuna bir arama yazdığında tooshove gerekir, toohello grafik API'si üzerinden.</span><span class="sxs-lookup"><span data-stu-id="4f4db-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="4f4db-200">Merhaba `GraphAPICaller` koddan hello oluşturacak, sınıf hello sunudan hello arama işlevselliği ayırır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="4f4db-201">Şimdilik, tüm arama karakter toohello grafik API'si akışları hello kod yazalım.</span><span class="sxs-lookup"><span data-stu-id="4f4db-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="4f4db-202">Adlı bir yöntem sağlayarak bunu `lookupInGraph`, toosearch için istiyoruz hello dizesini alır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="4f4db-203">Bir yardımcı sınıfı tooaccess hello grafik API'si yazma</span><span class="sxs-lookup"><span data-stu-id="4f4db-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="4f4db-204">Merhaba çekirdeği uygulamamız, budur.</span><span class="sxs-lookup"><span data-stu-id="4f4db-204">This is hello core of our application.</span></span> <span data-ttu-id="4f4db-205">Burada Hello rest kod hello varsayılan MVC örüntüsü Apple ekleme ancak hello kullanıcı türleri ve bu verileri döndürmek kod tooquery hello grafik yazma.</span><span class="sxs-lookup"><span data-stu-id="4f4db-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="4f4db-206">Merhaba kod işte ve ayrıntılı bir açıklama onu izler.</span><span class="sxs-lookup"><span data-stu-id="4f4db-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="4f4db-207">Yeni bir Objective C üst bilgi dosyası oluştur</span><span class="sxs-lookup"><span data-stu-id="4f4db-207">Create a new Objective C header file</span></span>
<span data-ttu-id="4f4db-208">Ad hello dosyası `GraphAPICaller.h`ve hello aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="4f4db-209">Burada belirtilen yöntem bir dize alır ve bir completionBlock döndürür bakın.</span><span class="sxs-lookup"><span data-stu-id="4f4db-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="4f4db-210">Tahmin şekilde bu completionBlock bir nesne doldurulan verileri gerçek zamanlı kullanıcı aramalarını hello gibi sağlayarak hello tablo güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="4f4db-211">Yeni bir Objective C dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f4db-211">Create a new Objective C file</span></span>
<span data-ttu-id="4f4db-212">Ad hello dosyası `GraphAPICaller.m`, yöntem aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


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

```

<span data-ttu-id="4f4db-213">Bu yöntem ayrıntılı aracılığıyla edelim.</span><span class="sxs-lookup"><span data-stu-id="4f4db-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="4f4db-214">Bu kod Hello çekirdek olduğu hello `NXOAuth2Request`, hello parametreleri alan yöntemi hello settings.plist dosyasında zaten tanımlı.</span><span class="sxs-lookup"><span data-stu-id="4f4db-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="4f4db-215">Merhaba ilk tooconstruct hello sağ grafik API çağrısı bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="4f4db-216">Aradığınız çünkü `/users`, toohello grafik API'si kaynak hello sürüm ile birlikte ekleyerek belirtin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="4f4db-217">Hello API geliştikçe değiştirebilirsiniz çünkü bunlar bir dış ayarları dosyasında algılama tooput yapar.</span><span class="sxs-lookup"><span data-stu-id="4f4db-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="4f4db-218">Ardından, toohello Graph API çağrısı de sağlanır toospecify parametreleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="4f4db-219">Bu *çok önemli* tüm URI olmayan uyumlu karakterlerin çalışma zamanında temizlendiği çünkü hello parametreleri'ı hello kaynak uç koymayın.</span><span class="sxs-lookup"><span data-stu-id="4f4db-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="4f4db-220">Tüm sorgu kodu hello parametrelerinde sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4f4db-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="4f4db-221">Bu çağrı fark edebilirsiniz bir `convertParamsToDictionary` henüz yazmadınız yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4f4db-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="4f4db-222">Şimdi hello hello dosyanın sonunda şimdi yapın:</span><span class="sxs-lookup"><span data-stu-id="4f4db-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="4f4db-223">Ardından, hello kullanalım `NXOAuth2Request` JSON biçiminde hello API öğesinden yöntemi tooget verileri yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f4db-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="4f4db-224">Son olarak, hello veri toohello MasterViewController dönüş nasıl konumundaki bakalım.</span><span class="sxs-lookup"><span data-stu-id="4f4db-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="4f4db-225">Hello veri sıralanmış olarak döndürür ve seri durumdan toobe gerekir ve bir nesne yüklenen bu hello MainViewController kullanmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f4db-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="4f4db-226">Bu amaçla hello çatıyı sahip bir `User.m/h` dosya bir kullanıcı nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4f4db-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="4f4db-227">Bu kullanıcı nesnesi hello grafik alınan bilgilerle doldurun.</span><span class="sxs-lookup"><span data-stu-id="4f4db-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a><span data-ttu-id="4f4db-228">Merhaba örnek çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4f4db-228">Run hello sample</span></span>
<span data-ttu-id="4f4db-229">Merhaba çatıyı kullanılan veya birlikte hello gözden geçirme ve ardından uygulamanızı şimdi çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f4db-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="4f4db-230">Merhaba simulator başlatır ve **oturum** toouse Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4f4db-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="4f4db-231">Ürünümüz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="4f4db-231">Get security updates for our product</span></span>
<span data-ttu-id="4f4db-232">Güvenlik olayları hello ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [güvenlik TechCenter](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="4f4db-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

