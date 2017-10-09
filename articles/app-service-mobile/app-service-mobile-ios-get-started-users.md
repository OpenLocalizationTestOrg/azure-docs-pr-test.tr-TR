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
# <a name="add-authentication-tooyour-ios-app"></a>Kimlik doğrulama tooyour iOS uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Bu öğretici kapsamında, kimlik doğrulama toohello ekleme [iOS Hızlı Başlat] desteklenen kimlik sağlayıcısı kullanarak proje. Bu öğretici hello üzerinde temel [iOS Hızlı Başlat] önce tamamlamanız gereken öğretici.

## <a name="register"></a>Kimlik doğrulaması için uygulamanızı kaydetmenizi ve hello uygulama hizmetini yapılandırma
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uygulama toohello izin verilen dış yönlendirme URL'lerini ekleme

Uygulamanız için yeni bir URL şemasını tanımlamak güvenli kimlik doğrulaması gerektirir.  Merhaba kimlik doğrulama işlemi tamamlandıktan sonra bu hello authentication sistem tooredirect geri tooyour uygulamasını sağlar.  Bu öğreticide, URL şemasının kullanırız _appname_ boyunca.  Ancak, seçtiğiniz herhangi bir URL şeması kullanabilirsiniz.  Benzersiz tooyour mobil uygulama olmalıdır.  th sunucu tarafı tooenable hello yönlendirme:

1. Merhaba, [Azure portal], uygulama hizmetinizi seçin.

2. Merhaba tıklatın **kimlik doğrulama / yetkilendirme** menü seçeneği.

3. Tıklatın **Azure Active Directory** hello altında **kimlik doğrulama sağlayıcıları** bölümü.

4. Set hello **yönetim modu** çok**Gelişmiş**.

5. Merhaba, **yeniden yönlendirme URL'lere izin**, girin `appname://easyauth.callback`.  Merhaba _appname_ bu içinde hello URL şeması mobil uygulamanız için bir dizedir.  Bir protokol (harf kullanın ve yalnızca sayı ve bir harf ile başlar) için normal URL belirtimi izlemelisiniz.  Merhaba çeşitli yerlerde URL şeması ile mobil uygulama kodunuzu tooadjust gerekeceğinden, seçtiğiniz hello dize Not olmanız gerekir.

6. **Tamam** düğmesine tıklayın.

7. **Kaydet** düğmesine tıklayın.

## <a name="permissions"></a>İzinleri tooauthenticated kullanıcılarını kısıtlayın
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Xcode'da, basın **çalıştırmak** toostart hello uygulama. Merhaba uygulama tooaccess arka ucu kimliği doğrulanmamış bir kullanıcı olarak çalıştığı bir özel durum oluşturulur, ancak hello *Todoıtem* tablo artık kimlik doğrulaması gerektirir.

## <a name="add-authentication"></a>Kimlik doğrulama tooapp Ekle
**Objective-C**:

1. Mac'inizde açmak *QSTodoListViewController.m* xcode'da ve yöntemi aşağıdaki hello ekleyin:

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

    Değişiklik *google* çok*microsoftaccount*, *twitter*, *facebook*, veya *windowsazureactivedirectory* kimlik sağlayıcınız olarak Google kullanmıyorsanız. Facebook kullanmak istiyorsanız, gerekir [beyaz liste Facebook etki alanları] [ 1] uygulamanızda.

    Hello yerine **urlScheme** uygulamanız için benzersiz bir ada sahip.  Merhaba urlScheme olması hello aynı hello hello belirtilen URL şeması protokolü olarak **yeniden yönlendirme URL'lere izin** hello Azure portal alanındaki. kimlik doğrulama isteği tamamlandıktan sonra hello urlScheme hello kimlik doğrulama geri çağırma tooswitch geri tooyour uygulama tarafından kullanılır.

2. Değiştir `[self refresh]` içinde `viewDidLoad` içinde *QSTodoListViewController.m* koddan hello ile:

    ```Objective-C
    [self loginAndGetData];
    ```

3. Açık hello `QSAppDelegate.h` dosya ve hello aşağıdaki kodu ekleyin:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Açık hello `QSAppDelegate.m` dosya ve hello aşağıdaki kodu ekleyin:

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

   Bu kodu doğrudan hello satır okuma önce ekleyin `#pragma mark - Core Data stack`.  Değiştir _appname_ 1. adımda kullanılan olan hello urlScheme değeri.

5. Açık hello `AppName-Info.plist` dosya (uygulamanızın hello adıyla değiştirerek AppName) ve kod aşağıdaki hello ekleyin:

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

    Bu kod içinde hello yerleştirilmelidir `<dict>` öğesi.  Hello yerine _appname_ dize (dizi için içinde **CFBundleURLSchemes**) 1. adımda seçtiğiniz hello uygulama adı ile.  Ayrıca bu hello plist Düzenleyicisi - hello tıklayarak değişiklik yapabilirsiniz `AppName-Info.plist` dosyasını XCode tooopen hello plist düzenleyicisinde.

    Hello yerine `com.microsoft.azure.zumo` dize **CFBundleURLName** , Apple ile paket tanımlayıcı.

6. Tuşuna *çalıştırmak* toostart hello uygulama ve oturum açın. Oturum açtıktan sonra mümkün tooview hello Yapılacaklar listesi olması ve güncelleştirmelerinin olması gerekir.

**SWIFT**:

1. Mac'inizde açmak *ToDoTableViewController.swift* xcode'da ve yöntemi aşağıdaki hello ekleyin:

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

    Değişiklik *google* çok*microsoftaccount*, *twitter*, *facebook*, veya *windowsazureactivedirectory* kimlik sağlayıcınız olarak Google kullanmıyorsanız. Facebook kullanmak istiyorsanız, gerekir [beyaz liste Facebook etki alanları] [ 1] uygulamanızda.

    Hello yerine **urlScheme** uygulamanız için benzersiz bir ada sahip.  Merhaba urlScheme olması hello aynı hello hello belirtilen URL şeması protokolü olarak **yeniden yönlendirme URL'lere izin** hello Azure portal alanındaki. kimlik doğrulama isteği tamamlandıktan sonra hello urlScheme hello kimlik doğrulama geri çağırma tooswitch geri tooyour uygulama tarafından kullanılır.

2. Merhaba satırları Kaldır `self.refreshControl?.beginRefreshing()` ve `self.onRefresh(self.refreshControl)` sonunda `viewDidLoad()` içinde *ToDoTableViewController.swift*. Çağrı çok ekleyin`loginAndGetData()` kendi yerinde:

    ```swift
    loginAndGetData()
    ```

3. Açık hello `AppDelegate.swift` dosya ve satır toohello aşağıdaki hello ekleyin `AppDelegate` sınıfı:

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

    Hello yerine _appname_ 1. adımda kullanılan olan hello urlScheme değeri.

4. Açık hello `AppName-Info.plist` dosya (uygulamanızın hello adıyla değiştirerek AppName) ve kod aşağıdaki hello ekleyin:

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

    Bu kod içinde hello yerleştirilmelidir `<dict>` öğesi.  Hello yerine _appname_ dize (dizi için içinde **CFBundleURLSchemes**) 1. adımda seçtiğiniz hello uygulama adı ile.  Ayrıca bu hello plist Düzenleyicisi - hello tıklayarak değişiklik yapabilirsiniz `AppName-Info.plist` dosyasını XCode tooopen hello plist düzenleyicisinde.

    Hello yerine `com.microsoft.azure.zumo` dize **CFBundleURLName** , Apple ile paket tanımlayıcı.

5. Tuşuna *çalıştırmak* toostart hello uygulama ve oturum açın. Oturum açtıktan sonra mümkün tooview hello Yapılacaklar listesi olması ve güncelleştirmelerinin olması gerekir.

Uygulama hizmeti kimlik doğrulama elmalar Inter uygulama iletişimi kullanır.  Bu konu hakkında daha fazla ayrıntı için toohello başvurun [Apple belgeleri][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure portal]: https://portal.azure.com

[iOS Hızlı Başlat]: app-service-mobile-ios-get-started.md

