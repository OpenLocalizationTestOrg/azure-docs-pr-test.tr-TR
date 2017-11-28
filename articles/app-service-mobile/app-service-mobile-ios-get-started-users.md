---
title: "İOS Azure Mobile Apps ile kimlik doğrulaması ekleme"
description: "İOS uygulamanızın kimlik sağlayıcıları, AAD, Google, Facebook, Twitter ve Microsoft dahil olmak üzere çeşitli kullanıcıların kimliklerini doğrulamak için Azure Mobile Apps kullanmayı öğrenin."
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
ms.openlocfilehash: 21a2cc6c1eaf4b34cbe8c2d7c4dbb69c8730cf32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="ae6c0-103">İOS uygulamanıza kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="ae6c0-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="ae6c0-104">Bu öğretici kapsamında, kimlik doğrulaması ekleme [iOS Hızlı Başlat] desteklenen kimlik sağlayıcısı kullanarak proje.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="ae6c0-105">Bu öğretici dayanır [iOS Hızlı Başlat] önce tamamlamanız gereken öğretici.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="ae6c0-106"><a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetme ve uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ae6c0-106"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="ae6c0-107"><a name="redirecturl"></a>Uygulamanız için izin verilen dış yönlendirme URL'leri ekleme</span><span class="sxs-lookup"><span data-stu-id="ae6c0-107"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="ae6c0-108">Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="ae6c0-109">Bu kimlik doğrulama işlemi tamamlandıktan sonra uygulamanıza geri yönlendirmek bir kimlik doğrulama sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="ae6c0-110">Bu öğreticide, URL şemasının kullanırız _appname_ boyunca.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="ae6c0-111">Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="ae6c0-112">Mobil uygulamanız için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="ae6c0-113">Th sunucu tarafında yeniden yönlendirmeyi etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="ae6c0-114">İçinde [Azure portal], uygulama hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="ae6c0-115">Tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="ae6c0-116">Tıklatın **Azure Active Directory** altında **kimlik doğrulama sağlayıcıları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="ae6c0-117">Ayarlama **yönetim modu** için **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="ae6c0-118">İçinde **yeniden yönlendirme URL'lere izin**, girin `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="ae6c0-119">_Appname_ Bu dize, mobil uygulamanız için URL düzenidir.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="ae6c0-120">Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="ae6c0-121">Çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu ayarlamak ihtiyaç duyacağınız seçtiğiniz dizeyi Not olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="ae6c0-122">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-122">Click **OK**.</span></span>

7. <span data-ttu-id="ae6c0-123">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-123">Click **Save**.</span></span>

## <span data-ttu-id="ae6c0-124"><a name="permissions"></a>Kimliği doğrulanmış kullanıcılar için izinleri kısıtla</span><span class="sxs-lookup"><span data-stu-id="ae6c0-124"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="ae6c0-125">Xcode'da, basın **çalıştırmak** uygulamayı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="ae6c0-126">Uygulama arka ucu kimliği doğrulanmamış bir kullanıcı olarak erişmeye çalıştığı bir özel durum oluşturulur ancak *Todoıtem* tablo artık kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="ae6c0-127"><a name="add-authentication"></a>Kimlik doğrulaması için uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="ae6c0-127"><a name="add-authentication"></a>Add authentication to app</span></span>
<span data-ttu-id="ae6c0-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-128">**Objective-C**:</span></span>

1. <span data-ttu-id="ae6c0-129">Mac'inizde açmak *QSTodoListViewController.m* xcode'da ve aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="ae6c0-130">Değişiklik *google* için *microsoftaccount*, *twitter*, *facebook*, veya *windowsazureactivedirectory* kimlik sağlayıcınız olarak Google kullanmıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ae6c0-131">Facebook kullanmak istiyorsanız, gerekir [beyaz liste Facebook etki alanları] [ 1] uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ae6c0-132">Değiştir **urlScheme** uygulamanız için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ae6c0-133">UrlScheme belirtilen URL şeması protokolü ile aynı olmalıdır **yeniden yönlendirme URL'lere izin** Azure portalında alan.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="ae6c0-134">UrlScheme kimlik doğrulama geri çağırmasının tarafından kimlik doğrulama isteği tamamlandıktan sonra geri uygulamanıza geçiş yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ae6c0-135">Değiştir `[self refresh]` içinde `viewDidLoad` içinde *QSTodoListViewController.m* aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="ae6c0-136">Açık `QSAppDelegate.h` dosya ve aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="ae6c0-137">Açık `QSAppDelegate.m` dosya ve aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

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

   <span data-ttu-id="ae6c0-138">Bu kod satırı okuma hemen öncesine eklemek `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="ae6c0-139">Değiştir _appname_ olan 1. adımda kullanılan urlScheme değeri.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="ae6c0-140">Açık `AppName-Info.plist` (uygulamanızın adıyla değiştirerek AppName) dosyasını bulun ve aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="ae6c0-141">Bu kod içinde yerleştirilmelidir `<dict>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="ae6c0-142">Değiştir _appname_ dize (dizi için içinde **CFBundleURLSchemes**) 1. adımda seçtiğiniz uygulama adı ile.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="ae6c0-143">Ayrıca bu plist Düzenleyicisi - tıklayarak değişiklik yapabilirsiniz `AppName-Info.plist` plist Düzenleyicisi'ni açmak için XCode dosyasında.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="ae6c0-144">Değiştir `com.microsoft.azure.zumo` dize **CFBundleURLName** , Apple ile paket tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="ae6c0-145">Tuşuna *çalıştırmak* uygulamayı başlatın ve sonra oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="ae6c0-146">Oturum açtıktan sonra Yapılacaklar listesi görebilir ve güncelleştirme yapmak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="ae6c0-147">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-147">**Swift**:</span></span>

1. <span data-ttu-id="ae6c0-148">Mac'inizde açmak *ToDoTableViewController.swift* xcode'da ve aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="ae6c0-149">Değişiklik *google* için *microsoftaccount*, *twitter*, *facebook*, veya *windowsazureactivedirectory* kimlik sağlayıcınız olarak Google kullanmıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ae6c0-150">Facebook kullanmak istiyorsanız, gerekir [beyaz liste Facebook etki alanları] [ 1] uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ae6c0-151">Değiştir **urlScheme** uygulamanız için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ae6c0-152">UrlScheme belirtilen URL şeması protokolü ile aynı olmalıdır **yeniden yönlendirme URL'lere izin** Azure portalında alan.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="ae6c0-153">UrlScheme kimlik doğrulama geri çağırmasının tarafından kimlik doğrulama isteği tamamlandıktan sonra geri uygulamanıza geçiş yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ae6c0-154">Satırları kaldırmak `self.refreshControl?.beginRefreshing()` ve `self.onRefresh(self.refreshControl)` sonunda `viewDidLoad()` içinde *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="ae6c0-155">Bir çağrı ekleyin `loginAndGetData()` kendi yerinde:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="ae6c0-156">Açık `AppDelegate.swift` dosya ve aşağıdaki satırı ekleyin `AppDelegate` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

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

    <span data-ttu-id="ae6c0-157">Değiştir _appname_ olan 1. adımda kullanılan urlScheme değeri.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="ae6c0-158">Açık `AppName-Info.plist` (uygulamanızın adıyla değiştirerek AppName) dosyasını bulun ve aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ae6c0-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="ae6c0-159">Bu kod içinde yerleştirilmelidir `<dict>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="ae6c0-160">Değiştir _appname_ dize (dizi için içinde **CFBundleURLSchemes**) 1. adımda seçtiğiniz uygulama adı ile.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="ae6c0-161">Ayrıca bu plist Düzenleyicisi - tıklayarak değişiklik yapabilirsiniz `AppName-Info.plist` plist Düzenleyicisi'ni açmak için XCode dosyasında.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="ae6c0-162">Değiştir `com.microsoft.azure.zumo` dize **CFBundleURLName** , Apple ile paket tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="ae6c0-163">Tuşuna *çalıştırmak* uygulamayı başlatın ve sonra oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="ae6c0-164">Oturum açtıktan sonra Yapılacaklar listesi görebilir ve güncelleştirme yapmak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="ae6c0-165">Uygulama hizmeti kimlik doğrulama elmalar Inter uygulama iletişimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="ae6c0-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="ae6c0-166">Bu konu hakkında daha fazla ayrıntı için başvurmak [Apple belgeleri][2]</span><span class="sxs-lookup"><span data-stu-id="ae6c0-166">For more details on this subject, refer to the [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
<span data-ttu-id="ae6c0-167">[Azure portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ae6c0-167">[Azure portal]: https://portal.azure.com</span></span>

<span data-ttu-id="ae6c0-168">[iOS Hızlı Başlat]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="ae6c0-168">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

