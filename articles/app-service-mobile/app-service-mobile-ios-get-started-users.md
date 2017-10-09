---
title: "Azure Mobile Apps ile iOS aaaAdd kimlik doğrulaması"
description: "Bilgi nasıl toouse Azure Mobile Apps tooauthenticate kimlik sağlayıcıları, AAD, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli, iOS uygulamanızın kullanıcılarının."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="b0868-103">Kimlik doğrulama tooyour iOS uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="b0868-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="b0868-104">Bu öğretici kapsamında, kimlik doğrulama toohello ekleme [iOS Hızlı Başlat] desteklenen kimlik sağlayıcısı kullanarak proje.</span><span class="sxs-lookup"><span data-stu-id="b0868-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="b0868-105">Bu öğretici hello üzerinde temel [iOS Hızlı Başlat] önce tamamlamanız gereken öğretici.</span><span class="sxs-lookup"><span data-stu-id="b0868-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="b0868-106"><a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve hello uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b0868-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="b0868-107"><a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme</span><span class="sxs-lookup"><span data-stu-id="b0868-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="b0868-108">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b0868-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="b0868-109">Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0868-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="b0868-110">Bu öğreticide, URL şemasının kullanırız _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="b0868-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="b0868-111">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0868-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="b0868-112">Benzersiz tooyour mobil uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0868-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="b0868-113">th sunucu tarafı tooenable hello yönlendirme:</span><span class="sxs-lookup"><span data-stu-id="b0868-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="b0868-114">Merhaba, [Azure portal], uygulama hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="b0868-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="b0868-115">Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="b0868-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="b0868-116">Tıklatın **Azure Active Directory** hello altında **kimlik doğrulama sağlayıcıları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b0868-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="b0868-117">Set hello **yönetim modu** çok**Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="b0868-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="b0868-118">Merhaba, **yeniden yönlendirme URL'lere izin**, girin `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="b0868-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="b0868-119">Merhaba _appname_ bu içinde hello URL şeması mobil uygulamanız için bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="b0868-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="b0868-120">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b0868-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="b0868-121">Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0868-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="b0868-122">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0868-122">Click **OK**.</span></span>

7. <span data-ttu-id="b0868-123">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0868-123">Click **Save**.</span></span>

## <span data-ttu-id="b0868-124"><a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın</span><span class="sxs-lookup"><span data-stu-id="b0868-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b0868-125">Xcode'da, basın **çalıştırmak** toostart hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="b0868-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="b0868-126">Merhaba uygulama tooaccess arka ucu kimliği doğrulanmamış bir kullanıcı olarak çalıştığı bir özel durum oluşturulur, ancak hello *Todoıtem* tablo artık kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b0868-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="b0868-127"><a name="add-authentication"></a>Kimlik doğrulama tooapp Ekle</span><span class="sxs-lookup"><span data-stu-id="b0868-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="b0868-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b0868-128">**Objective-C**:</span></span>

1. <span data-ttu-id="b0868-129">Mac'inizde açmak *QSTodoListViewController.m* xcode'da ve yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0868-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="b0868-130">Değişiklik *google* çok*microsoftaccount*, *twitter*, *facebook*, veya *windowsazureactivedirectory* kimlik sağlayıcınız olarak Google kullanmıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b0868-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="b0868-131">Facebook kullanmak istiyorsanız, gerekir [beyaz liste Facebook etki alanları] [ 1] uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="b0868-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="b0868-132">Hello yerine **urlScheme** uygulamanız için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="b0868-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="b0868-133">Merhaba urlScheme olması hello aynı hello hello belirtilen URL şeması protokolü olarak **yeniden yönlendirme URL'lere izin** hello Azure portal alanındaki.</span><span class="sxs-lookup"><span data-stu-id="b0868-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="b0868-134">kimlik doğrulama isteği tamamlandıktan sonra hello urlScheme hello kimlik doğrulama geri çağırma tooswitch geri tooyour uygulama tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0868-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="b0868-135">Değiştir `[self refresh]` içinde `viewDidLoad` içinde *QSTodoListViewController.m* koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="b0868-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="b0868-136">Açık hello `QSAppDelegate.h` dosya ve hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0868-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="b0868-137">Açık hello `QSAppDelegate.m` dosya ve hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0868-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="b0868-138">Bu kodu doğrudan hello satır okuma önce ekleyin `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="b0868-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="b0868-139">Değiştir _appname_ 1. adımda kullanılan olan hello urlScheme değeri.</span><span class="sxs-lookup"><span data-stu-id="b0868-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="b0868-140">Açık hello `AppName-Info.plist` dosya (uygulamanızın hello adıyla değiştirerek AppName) ve kod aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0868-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="b0868-141">Bu kod içinde hello yerleştirilmelidir `<dict>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="b0868-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="b0868-142">Hello yerine _appname_ dize (dizi için içinde **CFBundleURLSchemes**) 1. adımda seçtiğiniz hello uygulama adı ile.</span><span class="sxs-lookup"><span data-stu-id="b0868-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="b0868-143">Ayrıca bu hello plist Düzenleyicisi - hello tıklayarak değişiklik yapabilirsiniz `AppName-Info.plist` dosyasını XCode tooopen hello plist düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="b0868-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="b0868-144">Hello yerine `com.microsoft.azure.zumo` dize **CFBundleURLName** , Apple ile paket tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="b0868-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="b0868-145">Tuşuna *çalıştırmak* toostart hello uygulama ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b0868-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="b0868-146">Oturum açtıktan sonra mümkün tooview hello Yapılacaklar listesi olması ve güncelleştirmelerinin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0868-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="b0868-147">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="b0868-147">**Swift**:</span></span>

1. <span data-ttu-id="b0868-148">Mac'inizde açmak *ToDoTableViewController.swift* xcode'da ve yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0868-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="b0868-149">Değişiklik *google* çok*microsoftaccount*, *twitter*, *facebook*, veya *windowsazureactivedirectory* kimlik sağlayıcınız olarak Google kullanmıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b0868-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="b0868-150">Facebook kullanmak istiyorsanız, gerekir [beyaz liste Facebook etki alanları] [ 1] uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="b0868-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="b0868-151">Hello yerine **urlScheme** uygulamanız için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="b0868-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="b0868-152">Merhaba urlScheme olması hello aynı hello hello belirtilen URL şeması protokolü olarak **yeniden yönlendirme URL'lere izin** hello Azure portal alanındaki.</span><span class="sxs-lookup"><span data-stu-id="b0868-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="b0868-153">kimlik doğrulama isteği tamamlandıktan sonra hello urlScheme hello kimlik doğrulama geri çağırma tooswitch geri tooyour uygulama tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0868-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="b0868-154">Merhaba satırları Kaldır `self.refreshControl?.beginRefreshing()` ve `self.onRefresh(self.refreshControl)` sonunda `viewDidLoad()` içinde *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="b0868-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="b0868-155">Çağrı çok ekleyin`loginAndGetData()` kendi yerinde:</span><span class="sxs-lookup"><span data-stu-id="b0868-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="b0868-156">Açık hello `AppDelegate.swift` dosya ve satır toohello aşağıdaki hello ekleyin `AppDelegate` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b0868-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="b0868-157">Hello yerine _appname_ 1. adımda kullanılan olan hello urlScheme değeri.</span><span class="sxs-lookup"><span data-stu-id="b0868-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="b0868-158">Açık hello `AppName-Info.plist` dosya (uygulamanızın hello adıyla değiştirerek AppName) ve kod aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0868-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="b0868-159">Bu kod içinde hello yerleştirilmelidir `<dict>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="b0868-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="b0868-160">Hello yerine _appname_ dize (dizi için içinde **CFBundleURLSchemes**) 1. adımda seçtiğiniz hello uygulama adı ile.</span><span class="sxs-lookup"><span data-stu-id="b0868-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="b0868-161">Ayrıca bu hello plist Düzenleyicisi - hello tıklayarak değişiklik yapabilirsiniz `AppName-Info.plist` dosyasını XCode tooopen hello plist düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="b0868-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="b0868-162">Hello yerine `com.microsoft.azure.zumo` dize **CFBundleURLName** , Apple ile paket tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="b0868-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="b0868-163">Tuşuna *çalıştırmak* toostart hello uygulama ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b0868-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="b0868-164">Oturum açtıktan sonra mümkün tooview hello Yapılacaklar listesi olması ve güncelleştirmelerinin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0868-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="b0868-165">Uygulama hizmeti kimlik doğrulama elmalar Inter uygulama iletişimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0868-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="b0868-166">Bu konu hakkında daha fazla ayrıntı için toohello başvurun [Apple belgeleri][2]</span><span class="sxs-lookup"><span data-stu-id="b0868-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure portal]: https://portal.azure.com

[iOS Hızlı Başlat]: app-service-mobile-ios-get-started.md

