---
title: "aaaHow tooUse iOS için Azure Mobile Apps SDK'sı"
description: "Nasıl tooUse iOS için Azure Mobile Apps SDK'sı"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>Nasıl tooUse iOS için Azure Mobile Apps istemci kitaplığı
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Bu kılavuz hello son kullanarak tooperform genel senaryolar öğretilmektedir [Azure Mobile Apps iOS SDK'sı][1]. Yeni tooAzure mobil uygulamalar varsa, ilk tamamlamak [Azure Mobile Apps Hızlı Başlangıç] toocreate bir arka uç bir tablo oluşturun ve önceden derlenmiş iOS Xcode projenizi indirin. Bu kılavuzda, hello istemci-tarafı iOS SDK'sı odaklanın. toolearn hakkında daha fazla bilgi için hello arka uç sunucu tarafı SDK Merhaba, hello Server SDK HOWTOs bakın.

## <a name="reference-documentation"></a>Başvuru belgeleri
Merhaba başvuru belgeleri hello iOS istemci SDK'sı için aşağıda bulunur: [Azure Mobile Apps iOS istemci başvurusu][2].

## <a name="supported-platforms"></a>Desteklenen platformlar
Merhaba iOS SDK'sı iOS 8.0 veya sonraki sürümleri için Objective-C projeleri, Swift 2.2 projeler ve Swift 2.3 projeleri destekler.

Merhaba "sunucu akış" kimlik doğrulaması için kullanıcı Arabirimi sunulan hello bir Web görünümü kullanır.  Kimlik doğrulama başka bir yöntem gereklidir hello cihaz mümkün toopresent WebView UI değilse hello ürün dış hello kapsamını olmasıdır.  
Bu SDK böylece Gözcü türü veya benzer şekilde kısıtlı aygıtlar için uygun değil.

## <a name="Setup"></a>Kurulum ve Önkoşullar
Bu kılavuz, bir tablo ile bir arka uç oluşturduğunuzu varsayar. Bu kılavuz, o hello aynı şeması hello tablolar olarak bu öğreticiler tablolu varsayar. Bu kılavuz Ayrıca, kodunuzda, başvuru varsayar `MicrosoftAzureMobile.framework` ve içeri aktarma `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>Nasıl yapılır: istemci oluşturma
tooaccess projenizdeki Azure Mobile Apps arka oluşturma bir `MSClient`. Değiştir `AppUrl` hello uygulama URL'si ile. Bırakabilir `gatewayURLString` ve `applicationKey` boş. Kimlik doğrulaması için bir ağ geçidi ayarladıysanız, doldurmak `gatewayURLString` hello ağ geçidi URL'si.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**SWIFT**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>Nasıl yapılır: Tablo başvurusu oluşturma
tooaccess veya güncelleştirme veriler, bir başvuru toohello arka uç tablosu oluşturun. Değiştir `TodoItem` tablonuz hello adı

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**SWIFT**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Nasıl yapılır: veri sorgulama
toocreate bir veritabanı sorgusu sorgu hello `MSTable` nesnesi. Merhaba aşağıdaki sorgu tüm hello öğeleri alır `TodoItem` ve günlükleri hello her öğenin metni.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**SWIFT**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>Nasıl yapılır: Filtre veri döndürdü
toofilter sonuçları, birçok kullanılabilir seçeneğiniz vardır.

bir koşul kullanmak kullanarak toofilter bir `NSPredicate` ve `readWithPredicate`. döndürülen veri toofind yalnızca tamamlanmamış Yapılacaklar öğelerini Hello aşağıdaki filtreler.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**SWIFT**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>Nasıl yapılır: MSQuery kullanın
(sıralama dahil ve disk belleği), karmaşık bir sorgu oluşturmak tooperform bir `MSQuery` nesnesi, doğrudan veya bir koşulu kullanarak:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**SWIFT**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery`birkaç sorgu davranışları denetlemenize olanak tanır.

* Sonuçları sırasını belirtin
* Hangi alanların tooreturn sınırla
* Kaç tane tooreturn kayıtları sınırla
* Yanıtta toplam sayısı belirtin
* İstekte özel sorgu dizesi parametreleri belirtin
* Ek işlevler Uygula

Yürütme bir `MSQuery` çağırarak sorgu `readWithCompletion` hello nesne üzerinde.

## <a name="sorting"></a>Nasıl yapılır: MSQuery ile verileri sıralama
toosort sonuçları bir örneğe bakalım. toosort alan 'text' artan sonra 'Tamamlandı' azalan, çağırma `MSQuery` sözlüğüdür:

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**SWIFT**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>Nasıl yapılır: alanları sınırlayabilir ve sorgu dizesi parametreleri MSQuery ile genişletin
bir sorguda döndürülen toolimit alanları toobe hello hello alanların hello adlarını belirtin **selectFields** özelliği. Bu örnek yalnızca hello metin ve tamamlanan alanları döndürür:

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**SWIFT**:

```
query.selectFields = ["text", "complete"]
```

tooinclude ek sorgu dizesi parametreleri hello Server'daki (örneğin, özel bir sunucu tarafı komut dosyası bunları kullandığından) isteği, doldurmak `query.parameters` sözlüğüdür:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**SWIFT**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>Nasıl yapılır: sayfa boyutu yapılandırın
Azure Mobile Apps ile Merhaba sayfa boyutu denetimleri hello arka uç tablolar aynı anda çekilen kayıt sayısı hello. Bir arama çok`pull` veri hiçbir daha fazla kayıt toopull kadar bu sayfa boyutuna göre verileri, ardından toplu.

Sayfa boyutu kullanarak olası tooconfigure olan **MSPullSettings** aşağıda gösterildiği gibi. Merhaba varsayılan sayfa boyutu 50'dir ve isteğe bağlı olarak aşağıdaki hello örnek too3 değiştirir.

Farklı bir sayfa boyutu performans nedenleriyle yapılandırabilirsiniz. Çok sayıda küçük veri kayıt varsa, yüksek sayfa boyutu hello sunucu gidiş dönüş sayısını azaltır.

Bu ayar yalnızca hello sayfa boyutu hello istemci tarafında denetler. Merhaba istemci hello Mobile Apps arka desteklediğinden daha büyük sayfa için bir boyut isterse, hello sayfa boyutu hello maksimum hello arka uç tutulabilir yapılandırılmış toosupport olmasıdır.

Bu ayrıca hello ayardır *numarası* veri kayıtlarını, değil hello *bayt boyutu*.

Hello istemci sayfa boyutunu artırmak için hello sunucuda hello sayfa boyutunu artırmanız gerekir. Bkz: ["nasıl yapılır: hello tablo disk belleği boyutunu Ayarla"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello toodo bu adımları için.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**SWIFT**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>Nasıl yapılır: Veri Ekle
Yeni bir tablo satırının tooinsert oluşturma bir `NSDictionary` ve çağırma `table insert`. Varsa [dinamik şema] olduğu etkin hello Azure App Service mobil arka uç otomatik olarak yeni sütunlar üzerinde hello dayalı oluşturur `NSDictionary`.

Varsa `id` hello arka uç otomatik olarak yeni bir benzersiz kimlik oluşturur değil sağlanır Kendi sağlamak `id` toouse e-posta adresleri, kullanıcı adlarını veya kendi özel değerlerinizi kimliği olarak Kendi Kimliğinizi sağlayarak, birleştirmeler ve işle ilgili veritabanı mantığı kolaylaştırır.

Merhaba `result` eklenmiş hello yeni öğe içeriyor. Sunucu mantığınızı bağlı olarak ek olabilir veya karşılaştırıldığında değiştirilen verileri toowhat toohello sunucu geçirildi.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**SWIFT**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>Nasıl yapılır: verileri değiştirme
bir öğe ve çağrı tooupdate var olan bir satır değiştirme `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**SWIFT**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

Alternatif olarak, hello satır kimliği ve güncelleştirilmiş hello alan sağlayın:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**SWIFT**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

En azından hello `id` güncelleştirmeleri yaparken özniteliği ayarlanmalıdır.

## <a name="deleting"></a>Nasıl yapılır: verileri Sil
bir öğeyi, toodelete çağırma `delete` hello öğe:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**SWIFT**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Alternatif olarak, satır kimliği sağlayarak Sil:

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**SWIFT**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

En azından hello `id` yapma sildiğinde özniteliği ayarlanmalıdır.

## <a name="customapi"></a>Nasıl yapılır: özel API çağrısı
Özel bir API ile herhangi bir arka uç işlevsellik getirebilir. Toomap tooa tablo işlemi yok. Yalnızca ileti üzerinde daha fazla denetim kazanmak yapın, hatta okuma/kümesi üstbilgileri ve hello yanıt gövdesi biçimini değiştirin. nasıl toocreate özel bir API hello arka uç üzerinde okuma toolearn [özel API'leri](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

toocall özel bir API çağrısı `MSClient.invokeAPI`. Merhaba istek ve yanıt içerik JSON olarak kabul edilir. toouse diğer medya türleri [kullanım hello diğer aşırı yüklemesini `invokeAPI` ] [ 5].  toomake bir `GET` yerine isteği bir `POST` isteği, kümesi parametresi `HTTPMethod` çok`"GET"` ve parametre `body` çok`nil` (GET istekleri İleti gövdeleri değil olduğundan.) Özel API'nizi diğer HTTP fiilleri destekliyorsa, değiştirme `HTTPMethod` uygun şekilde.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**SWIFT**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>Nasıl yapılır: yazmaç anında iletme şablonları toosend platformlar arası bildirimleri
tooregister şablonları şablonlarıyla geçirmek, **client.push registerDeviceToken** istemci uygulamanızı yöntemi.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**SWIFT**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

Şablonlarınızı türü NSDictionary ve birden fazla şablon içinde biçimini izleyen hello içerebilir:

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**SWIFT**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Tüm etiketleri güvenlik hello isteğinden kaldırılır.  tooadd etiketler tooinstallations veya yüklemeleri içinde şablonları için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][4].  kayıtlı bu şablonları kullanarak toosend bildirimleri çalışabilirsiniz [bildirim hub'ları API'leri][3].

## <a name="errors"></a>Nasıl yapılır: hata işleme
Azure uygulama hizmeti mobil arka uç çağırdığınızda hello tamamlama bloğu içeren bir `NSError` parametresi. Hata oluştuğunda, bu parametre nil olmayan olur. Kodunuzda bu parametreyi denetleyin ve kod parçacıkları önceki hello gösterildiği gibi gerektiğinde Merhaba hatayı işleyebilir.

Merhaba dosya [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] hello sabitleri tanımlar `MSErrorResponseKey`, `MSErrorRequestKey`, ve `MSErrorServerItemKey`. tooget ilgili daha fazla verileri toohello hata:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**SWIFT**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

Ayrıca, her hata kodunu sabitleri hello dosya tanımlar:

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**SWIFT**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Nasıl yapılır: kullanıcıların hello Active Directory kimlik doğrulama kitaplığı ile kimlik doğrulaması
Azure Active Directory'yi kullanarak uygulamanıza hello Active Directory Authentication Library (ADAL) toosign kullanıcılar kullanabilir. Bir kimlik sağlayıcısı SDK kullanarak istemci akış kimlik doğrulaması olan tercih toousing hello `loginWithProvider:completion:` yöntemi.  İstemci akış kimlik doğrulaması daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.

1. Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna AAD oturum açma için yapılandırma [tooconfigure App Service nasıl Active Directory oturum açma için] [ 7] Öğreticisi. Yerel istemci uygulaması kaydı emin toocomplete hello isteğe bağlı adım olun. İOS için öneririz URI'dir hello biçiminde o hello yeniden yönlendirme `<app-scheme>://<bundle-id>`. Daha fazla bilgi için bkz: Merhaba [ADAL iOS quickstart][8].
2. ADAL Cocoapods kullanarak yükleyin. Tanımı aşağıdaki, değiştirme, Podfile tooinclude hello Düzenle **YOUR proje** Xcode projenizi hello adı:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   ve Pod hello:

        pod 'ADALiOS'
3. Çalıştırma hello Terminali kullanarak `pod install` hello dizininden projenizi içeren ve oluşturulan hello Xcode çalışma alanı (Merhaba proje değil) açın.
4. Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello dil according hello ekleyin. Her, bu değişiklikleri yapın:

   * Değiştir **INSERT yetkilisi burada** uygulamanızı sağlanan hello Kiracı hello adı. Https://login.microsoftonline.com/contoso.onmicrosoft.com biçiminde olmalıdır. Bu değer, hello etki alanı sekmesinden hello [Klasik Azure portalı] Azure Active Directory'yi kopyalanabilir.
   * Değiştir **Ekle-RESOURCE-kimliği-Buraya** , mobil uygulamanızın arka ucuna için hello istemci kimliği. İstemci kimliği hello edinebilirsiniz **Gelişmiş** altında sekmesinde **Azure Active Directory ayarları** hello Portalı'nda.
   * Değiştir **Ekle-istemci-kimliği-Buraya** hello yerel istemci uygulamasından kopyaladığınız hello istemci kimliği.
   * Değiştir **Ekle-REDIRECT-URI-Buraya** sitenizin ile */.auth/login/done* hello HTTPS şeması kullanarak uç nokta. Bu değer çok benzer olmalıdır*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**SWIFT**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>Nasıl yapılır: Merhaba Facebook SDK'sı iOS için kullanıcılara kimlik doğrulaması
Facebook kullanarak uygulamanıza hello Facebook SDK'sı iOS toosign kullanıcılar için kullanabilirsiniz.  Bir istemci akış kimlik doğrulaması kullanmaktır tercih toousing hello `loginWithProvider:completion:` yöntemi.  Merhaba istemci akış kimlik doğrulaması daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.

1. İzleyerek, mobil uygulamanızın arka ucuna Facebook oturum açma için yapılandırma [tooconfigure App Service nasıl Facebook oturum açma için] [ 9] Öğreticisi.
2. Merhaba Facebook SDK'sı iOS için aşağıdaki hello tarafından yüklemek [Facebook SDK'sı iOS - Getting Started] [ 10] belgeleri. Bir uygulama oluşturmak yerine hello iOS platformu tooyour mevcut kayıt ekleyebilirsiniz.
3. Facebook'ın belgeleri hello uygulama temsilci bazı Objective-C kodunu içerir. Kullanıyorsanız **Swift**, çevirileri AppDelegate.swift için aşağıdaki hello kullanabilirsiniz:

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. Toplama tooadding içinde `FBSDKCoreKit.framework` tooyour projesi, ayrıca bir başvuru çok ekleyin`FBSDKLoginKit.framework` hello de aynı şekilde.
5. Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello dil according hello ekleyin.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**SWIFT**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>Nasıl yapılır: iOS için kullanıcılara Twitter doku ile kimlik doğrulaması
Twitter kullanarak uygulamanıza iOS toosign kullanıcılar için doku kullanabilirsiniz. İstemci akış kimlik doğrulamasıdır tercih toousing hello `loginWithProvider:completion:` şekliyle yöntemi daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.

1. Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna Twitter oturum açma için yapılandırma [tooconfigure App Service nasıl Twitter oturum açma için](app-service-mobile-how-to-configure-twitter-authentication.md) Öğreticisi.
2. Doku tooyour projesi tarafından aşağıdaki hello eklemek [iOS - Getting Started için doku] belgeleri ve TwitterKit ayarlama.

   > [!NOTE]
   > Varsayılan olarak, doku bir Twitter uygulaması sizin için oluşturur. Merhaba tüketici anahtarı ve tüketici önceki kod parçacıkları aşağıdaki hello kullanılarak oluşturulan gizli kaydederek bir uygulama oluşturmaya önleyebilirsiniz.    Alternatif olarak, hello tüketici anahtarı değiştirebilir ve tüketici gizli anahtarı değerlerini tooApp hizmeti ile Merhaba değerleri sağlayın görmek hello [doku Panosu]. Bu seçeneği seçerseniz, emin tooset hello geri çağırma URL'si tooa yer tutucu değerini, aşağıdaki gibi olması `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    Daha önce oluşturduğunuz hello gizli toouse seçerseniz, aşağıdaki kodu tooyour uygulama temsilci hello ekleyin:

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **SWIFT**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Kod tooyour uygulama aşağıdaki, kullanmakta olduğunuz toohello dil according hello ekleyin.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**SWIFT**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>Nasıl yapılır: kullanıcılar iOS için hello Google oturum açma SDK ile kimlik doğrulaması
Bir Google hesabı kullanarak uygulamanıza hello Google oturum açma SDK iOS toosign kullanıcılar için kullanabilirsiniz.  Google en son değişiklikleri tootheir OAuth güvenlik ilkeleri duyurdu.  Bu ilke değişikliklerini gelecekteki hello Google SDK'da hello kullanımını gerektirir.

1. Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna Google oturum açma için yapılandırma [tooconfigure App Service nasıl Google oturum açma için](app-service-mobile-how-to-configure-google-authentication.md) Öğreticisi.
2. Merhaba Google SDK'sı iOS için aşağıdaki hello tarafından yüklemek [Google oturum açma iOS için-başlangıç tümleştirme](https://developers.google.com/identity/sign-in/ios/start-integrating) belgeleri. "Merhaba kimlik doğrulaması ile bir arka uç sunucu" bölümüne atlayabilirsiniz.
3. Tooyour temsilcinin aşağıdaki hello eklemek `signIn:didSignInForUser:withError:` yöntemi, kullanmakta olduğunuz toohello dil göre.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**SWIFT**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Ayrıca ekleyin hello çok aşağıdaki emin olun`application:didFinishLaunchingWithOptions:` uygulamanızda temsilci, "SERVER_CLIENT_ID" hello ile değiştiriliyor aynı Bu, kullanılan tooconfigure uygulama hizmeti 1. adımda kimliği.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **SWIFT**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Kod tooyour hello uygulayan bir UIViewController uygulamasında aşağıdaki hello eklemek `GIDSignInUIDelegate` protokolü, kullanmakta olduğunuz toohello dil göre.  Yeniden imzalanmakta önce oturumu kapattınız ve kimlik bilgilerinizi yeniden tooenter gerekmeyen karşın, bir onay iletişim kutusu görebilirsiniz.  Merhaba Oturum belirteci süresi dolan yalnızca bu yöntemi çağırın.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **SWIFT**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure Mobile Apps Hızlı Başlangıç]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[dinamik şema]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[doku Panosu]: https://www.fabric.io/home
[iOS - Getting Started için doku]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
