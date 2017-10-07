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
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Grafik API'si hello v2.0 uç kullanarak bir üçüncü taraf kitaplık kullanılarak oturum açma tooan iOS uygulaması ekleyin
Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır. Geliştiricilerin hizmetlerimizle ile toointegrate istedikleri herhangi bir kitaplığı kullanabilirsiniz. toohelp geliştiricilerin platformumuzu diğer kitaplıklarla birlikte kullanmak, biz bu bir toodemonstrate gibi birkaç izlenecek nasıl yazdıktan tooconfigure üçüncü taraf kitaplıklar tooconnect toohello Microsoft kimlik platformu. Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) toohello Microsoft kimlik platformu bağlanabilir.

Bu izlenecek yol oluşturur hello uygulamasıyla kullanıcılar tootheir kuruluşunuzda oturum ve ardından başkaları için kuruluşlarında hello grafik API'sini kullanarak arama.

Yeni tooOAuth2 veya Openıd Connect değilseniz, bu örnek yapılandırmanın çoğunu algılama tooyou oluşturamazsınız. Okumanızı öneririz [v2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md) arka planı için.

> [!NOTE]
> Merhaba OAuth2 veya Openıd Connect standartları, koşullu erişim ve Intune ilke yönetimi gibi bir ifadeye sahip bazı özellikleri, bizim açık kaynak Microsoft Azure kimlik kitaplıkları, toouse gerektirir.
> 
> 

Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez.

> [!NOTE]
> Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Github'dan kodu indirme
Bu öğretici için kod Hello korunduğu [github'da](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

Hello örnek ayrıca indirebilirsiniz ve hemen başlayın:

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Bir uygulamayı kaydetme
Merhaba yeni bir uygulama oluşturma [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya ayrıntılı adımları hello izleyin [nasıl tooregister hello v2.0 uç noktası ile uygulama](active-directory-v2-app-registration.md).  Emin olun:

* Kopya hello **uygulama kimliği** , olduğundan atanan tooyour uygulama yakında gerekir.
* Merhaba eklemek **mobil** uygulamanız için platform.
* Kopya hello **yeniden yönlendirme URI'si** hello portalından. Merhaba varsayılan değeri kullanın `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Merhaba üçüncü taraf NXOAuth2 kitaplık indirmeniz ve çalışma alanı oluşturma
Bu kılavuz için github'dan Mac OS X ve iOS (Cocoa ve Cocoa touch) için bir OAuth2 kitaplığı olan OAuth2Client hello kullanır. Bu kitaplık hello OAuth2 belirtimi taslak 10 temel alır. Merhaba yerel uygulama profilini uygular ve hello hello kullanıcı yetkilendirme uç noktasını destekler. Bunlar hello Microsoft identity platformu ile toointegrate gerekir tüm hello noktalardır.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>CocoaPods kullanarak Hello kitaplığı tooyour projesi ekleyin
CocoaPods, Xcode projeleri için bir bağımlılık yöneticisidir. Merhaba önceki yükleme adımlarını otomatik olarak yönetir.

```
$ vi Podfile
```
1. Toothis podfile aşağıdaki hello ekleyin:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. CocoaPods kullanarak Hello podfile dosyasını yükleyin. Bu, yükleyeceğiniz yeni bir Xcode çalışma alanı oluşturur.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Merhaba projenin Hello yapısı keşfedin
Yapı izlenerek hello hello çatıyı bizim proje için kurun:

* UPN arama ile ana görünüm
* Merhaba veriler için ayrıntılı görünüm hello seçili kullanıcı hakkında
* Bir oturum açma kullanıcı toohello uygulama tooquery hello grafiğinde burada oturum görünümü

Biz hello iskelet tooadd kimlik doğrulaması toovarious dosyalarında taşınır. Diğer bölümleri hello görsel kod gibi hello kod tooidentity ilgilidir değil ancak sizin için sağlanır.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Merhaba Kitaplığı'nda hello settings.plst dosya ayarlama
* Merhaba Hello hızlı başlangıç projesi açmak `settings.plist` dosya. Hello Azure portal kullanılan hello bölüm tooreflect hello değerleri hello öğelerinde Hello değerlerini değiştirin. Merhaba Active Directory kimlik doğrulama kitaplığı kullandığında kodunuzu bu değerleri başvurur.
  * Merhaba `clientId` hello portalından kopyalandığından, uygulamanızın hello istemci kimliği.
  * Merhaba `redirectUri` hello yeniden yönlendirme URL'si sağlanan bu hello portalıdır.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Merhaba, LoginViewController içinde NXOAuth2Client kitaplığınızı ayarlayın
Merhaba NXOAuth2Client kitaplığınızı ayarlayın bazı değerler tooget gerektirir. Bu görev tamamlandıktan sonra hello alınan belirteç toocall hello grafik API'sini kullanabilirsiniz. Çünkü `LoginView` dilediğiniz zaman çağrılacağı tooauthenticate ihtiyacımız, tooput yapılandırma değerlerini toothat dosyasında mantıklıdır.

* Bazı değerler toohello ekleyelim `LoginViewController.m` kimlik doğrulama ve yetkilendirme için dosya tooset hello bağlamı. Merhaba değerleri ayrıntılarını hello kod izleyin.
  
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

Merhaba kod ayrıntılarını bakalım.

Merhaba ilk dizesi içindir `scopes`.  Merhaba `User.Read` değeri tooread hello temel profilini kullanıcı imzalı hello sağlar.

Tüm hello kullanılabilir kapsamların hakkında daha fazla bilgiyi [Microsoft Graph izin kapsamları](https://graph.microsoft.io/docs/authorization/permission_scopes).

İçin `authURL`, `loginURL`, `bhh`, ve `tokenURL`, daha önce sağlanan hello değerleri kullanmanız gerekir. Merhaba açık kaynak Microsoft Azure kimlik kitaplıklarını kullanırsanız, size bu verileri sizin için bizim meta veri uç noktasının kullanarak çekme. Biz bu değerleri sizin yerinize ayıklamak hello sabit iş yaptık.

Merhaba `keychain` değerdir NXOAuth2Client kitaplığının hello hello kapsayıcı toocreate Anahtarlık toostore belirteçlerinizi kullanır. Belirleyebileceğiniz tooget çoklu oturum açma (SSO) çok sayıda uygulamada istiyorsanız, hello uygulamalarınızın her birinde aynı Anahtarlıkta ve istek hello kullanılmasını Xcode yetkilendirmeler içinde. Bu hello Apple belgelerinde açıklanmıştır.

Bu değerlerin Hello rest gerekli toouse hello kitaplıkta ve toocarry değerleri toohello bağlamı yerler oluşturduğunuz.

### <a name="create-a-url-cache"></a>Bir URL önbelleği oluşturma
İçinde `(void)viewDidLoad()`, her zaman adlandırılan hello görünüm yüklendikten sonra hello aşağıdaki kodu primes bizim kullanmak için bir önbellek.

Hello aşağıdaki kodu ekleyin:

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

### <a name="create-a-webview-for-sign-in"></a>Oturum açma için bir Web görünümü oluşturma
Bir Web görünümü hello kullanıcıdan SMS metin iletisi (yapılandırılmışsa) gibi ek faktörler veya hata iletilerini toohello kullanıcıyı döndürür. Burada, hello WebView ve daha sonra yazma hello yedekleme olacağını kod toohandle hello geri aramalar hello WebView hello kimlik Hizmetleri'nden ayarlarsınız.

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

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Merhaba WebView yöntemlerini toohandle kimlik doğrulama geçersiz kıl
tootell hello daha önce anlatıldığı gibi bir kullanıcı olarak toosign gerektiğinde ne olacağını WebView, koddan hello yapıştırabilirsiniz.

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

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Kod toohandle hello hello OAuth2 isteğinin sonucunu yazma
Merhaba aşağıdaki kodu WebView hello döndürür hello Redirecturl'yi işleyecek. Kimlik doğrulaması başarısız olmadıysa hello kodu yeniden deneyecek. Bu sırada, hello kitaplığı hello konsolda görebileceğiniz veya zaman uyumsuz olarak işlemek hello hata sağlar.

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

### <a name="set-up-hello-oauth-context-called-account-store"></a>OAuth (hesap deposu olarak adlandırılır) bağlam Hello ayarlayın
Burada çağırabilirsiniz `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` hello paylaşılan hesap deposu hello uygulama toobe mümkün tooaccess istediğiniz her hizmet için. Merhaba hesap türü için belirli bir hizmeti bir tanımlayıcı olarak kullanılan bir dizedir. Hello grafik API'si eriştiğiniz çünkü hello kod olarak tooit başvuruyor `"myGraphService"`. Ardından herhangi bir şey hello belirteciyle değiştirildiğinde bildirir bir gözlemci ayarlanır. Merhaba belirteci aldıktan sonra hello kullanıcı geri toohello iade `masterView`.

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Ana görünüm toosearch Hello ayarlayın ve hello grafik API'si hello kullanıcıları görüntüle
Döndürülen veriler hello kılavuzunda hello görüntüleyen bir ana-View-Controller (MVC) uygulama hello bu kılavuz kapsamında değildir ve birçok çevrimiçi eğitim açıklama nasıl toobuild biri. Bu kod hello iskelet dosyasıdır. Ancak, bu MVC uygulamasındaki birkaç şey ile toodeal gerekir:

* Bir kullanıcı bir şey hello arama alanına yazdığında müdahale
* Bir nesneyi veri arka toohello MasterView hello kılavuzunda hello sonuçları görüntüleyebilmesi sağlayın

Biz bu aşağıdaki gerçekleştirirsiniz.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Oturum açtınız varsa onay toosee ekleyin.
Merhaba kullanıcı, imzalı değilse zaten varsa bir simge hello önbelleğinde akıllı toocheck olacak şekilde hello uygulama az yapar. Toohello LoginView hello kullanıcı toosign için yönlendirme değil, varsa. Geri çağırma bir görünüm yüklenirken hello en iyi şekilde toodo eylemler varsa, toouse hello `viewDidLoad()` Apple bize sağlayan yöntemidir.

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

### <a name="update-hello-table-view-when-data-is-received"></a>Güncelleştirme hello tablo veri alındığında görünümü
Merhaba grafik API'si veri döndürdüğünde toodisplay hello veri gerekir. Kolaylık olması için burada tüm hello kodu tooupdate hello tablosu verilmiştir. MVC Demirbaş kodunuzda hello doğru değerleri yalnızca yapıştırabilirsiniz.

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

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Birisi hello arama alanına yazdığında bir şekilde toocall hello grafik API'si sağlayın
Bir kullanıcı hello kutusuna bir arama yazdığında tooshove gerekir, toohello grafik API'si üzerinden. Merhaba `GraphAPICaller` koddan hello oluşturacak, sınıf hello sunudan hello arama işlevselliği ayırır. Şimdilik, tüm arama karakter toohello grafik API'si akışları hello kod yazalım. Adlı bir yöntem sağlayarak bunu `lookupInGraph`, toosearch için istiyoruz hello dizesini alır.

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Bir yardımcı sınıfı tooaccess hello grafik API'si yazma
Merhaba çekirdeği uygulamamız, budur. Burada Hello rest kod hello varsayılan MVC örüntüsü Apple ekleme ancak hello kullanıcı türleri ve bu verileri döndürmek kod tooquery hello grafik yazma. Merhaba kod işte ve ayrıntılı bir açıklama onu izler.

### <a name="create-a-new-objective-c-header-file"></a>Yeni bir Objective C üst bilgi dosyası oluştur
Ad hello dosyası `GraphAPICaller.h`ve hello aşağıdaki kodu ekleyin.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Burada belirtilen yöntem bir dize alır ve bir completionBlock döndürür bakın. Tahmin şekilde bu completionBlock bir nesne doldurulan verileri gerçek zamanlı kullanıcı aramalarını hello gibi sağlayarak hello tablo güncelleştirir.

### <a name="create-a-new-objective-c-file"></a>Yeni bir Objective C dosyası oluşturma
Ad hello dosyası `GraphAPICaller.m`, yöntem aşağıdaki hello ekleyin.

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

Bu yöntem ayrıntılı aracılığıyla edelim.

Bu kod Hello çekirdek olduğu hello `NXOAuth2Request`, hello parametreleri alan yöntemi hello settings.plist dosyasında zaten tanımlı.

Merhaba ilk tooconstruct hello sağ grafik API çağrısı bir adımdır. Aradığınız çünkü `/users`, toohello grafik API'si kaynak hello sürüm ile birlikte ekleyerek belirtin. Hello API geliştikçe değiştirebilirsiniz çünkü bunlar bir dış ayarları dosyasında algılama tooput yapar.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Ardından, toohello Graph API çağrısı de sağlanır toospecify parametreleri gerekir. Bu *çok önemli* tüm URI olmayan uyumlu karakterlerin çalışma zamanında temizlendiği çünkü hello parametreleri'ı hello kaynak uç koymayın. Tüm sorgu kodu hello parametrelerinde sağlanmalıdır.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

Bu çağrı fark edebilirsiniz bir `convertParamsToDictionary` henüz yazmadınız yöntemi. Şimdi hello hello dosyanın sonunda şimdi yapın:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Ardından, hello kullanalım `NXOAuth2Request` JSON biçiminde hello API öğesinden yöntemi tooget verileri yedekleyin.

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

Son olarak, hello veri toohello MasterViewController dönüş nasıl konumundaki bakalım. Hello veri sıralanmış olarak döndürür ve seri durumdan toobe gerekir ve bir nesne yüklenen bu hello MainViewController kullanmasını sağlayabilirsiniz. Bu amaçla hello çatıyı sahip bir `User.m/h` dosya bir kullanıcı nesnesi oluşturur. Bu kullanıcı nesnesi hello grafik alınan bilgilerle doldurun.

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


## <a name="run-hello-sample"></a>Merhaba örnek çalıştırın
Merhaba çatıyı kullanılan veya birlikte hello gözden geçirme ve ardından uygulamanızı şimdi çalıştırmanız gerekir. Merhaba simulator başlatır ve **oturum** toouse Merhaba uygulaması.

## <a name="get-security-updates-for-our-product"></a>Ürünümüz için güvenlik güncelleştirmelerini alma
Güvenlik olayları hello ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [güvenlik TechCenter](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.

