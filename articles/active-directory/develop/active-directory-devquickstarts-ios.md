---
title: "bir iOS uygulaması içine aaaIntegrate Azure AD | Microsoft Docs"
description: "Nasıl toobuild oturum açma ve Azure AD aramalar için Azure AD ile tümleşen bir iOS uygulaması API'leri OAuth kullanılarak korunan."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>Azure AD bir iOS uygulamanıza tümleştirmek
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Bizim yeni Hello önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/iOS) yardımcı olan Azure Active Directory ile yalnızca birkaç dakika içinde başlamak ve çalıştırmak!  Hello Geliştirici Portalı bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme hello işleminde size kılavuzluk eder.  İşiniz bittiğinde, bu belirteçleri kabul edebilir ve doğrulama gerçekleştirmek kullanıcılar, Kiracı ve arka uç kimlik doğrulaması yapabilir basit bir uygulama gerekir. 
> 
> 

Azure Active Directory (Azure AD) tooaccess gereken iOS istemciler korunan kaynakları hello Active Directory kimlik doğrulama kitaplığı ya da ADAL sağlar. ADAL uygulamanızı tooobtain erişim belirteçleri kullandığını hello işlemini basitleştirir. toodemonstrate olduğu, bu makaledeki ne kadar kolay bir hedefi C Yapılacaklar listesi uygulaması, biz oluşturma:

* Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Belirtilen diğer ada sahip kullanıcılar için bir dizin arar.

toobuild hello tam çalışan bir uygulama şunları yapmanız gerekir:

1. Uygulamanızı Azure AD ile kaydedin.
2. Yükleyin ve ADAL yapılandırın.
3. Azure AD'den ADAL tooget belirteçleri kullanın.

başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). Ayrıca kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir. Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).


> [!TIP]
> Bizim yeni Hello önizlemesini denemek [Geliştirici Portalı](https://identity.microsoft.com/Docs/iOS) yardımcı olan birkaç dakika içinde Azure AD ile başlamak ve çalıştırmak. Hello Geliştirici Portalı bir uygulamayı kaydetme ve Azure AD kodunuza tümleştirme hello işleminde size kılavuzluk eder. Kullanıcıların kiracınızda doğrulanabilir basit bir uygulamanız varsa ve bir arka uç tamamlanmış olduğunuzda, belirteçleri kabul edebilir ve doğrulama yapmak. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. İOS için URI'dir, yönlendirme belirleme
toosecurely belirli SSO senaryolarda uygulamalarınızın Başlat, oluşturmanız gerekir bir *yeniden yönlendirme URI'si* belirli bir biçimde. Bir yeniden yönlendirme URI'si için bunları sorulan belirteçleri dönüş toohello doğru uygulama hello kullanılan tooensure ' dir.


Hello iOS için bir yeniden yönlendirme URI'si biçimdir:

```
<app-scheme>://<bundle-id>
```

* **Uygulama düzeni** -Bu, XCode projenizde kayıtlı değil. Bu, nasıl diğer uygulamaları çağırabilirsiniz olur. Bulabileceğiniz bu Info.plist altında -> URL türleri -> URL tanımlayıcısı. Bir veya daha fazla yapılandırılmış henüz yoksa bir oluşturmanız gerekir.
* **paket kimliği** -hello paket "kimlik" altında bulunan tanımlayıcısı budur kaydını proje ayarlarınızı xcode'da.

Bu hızlı başlangıç kodun bir örnek: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2. Merhaba DirectorySearcher uygulamayı Kaydet
tooset uygulama tooget belirteçleri yukarı ilk ihtiyacınız tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst çubuğunda hesabınızı tıklatın. Merhaba altında **Directory** listesinde, uygulamanızın hello Active Directory Kiracı tooregister istediğiniz yeri seçin.
3. Tıklatın **daha Hizmetleri** hello Soldaki gezinti bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. İzleyin hello ister yeni bir toocreate **yerel istemci uygulaması**.
  * Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın açıklar.
  * Merhaba **yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanan bir şema ve dize birleşimidir.  Belirli tooyour uygulama ve hello önceki yeniden yönlendirme URI'si bilgiyi temel alan bir değer girin.
6. Merhaba kaydı tamamladıktan sonra Azure AD, uygulamanızın benzersiz uygulama kimliği atar.  Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.
7. Merhaba gelen **ayarları** sayfasında, **gerekli izinler** ve ardından **Ekle**. Seçin **Microsoft Graph** API, hello gibi hello ekleyin **dizin verilerini okuma** altında izni **izinlere temsilci**.  Bu, kullanıcılar için Azure AD Graph API uygulaması tooquery hello ayarlar.

## <a name="3-install-and-configure-adal"></a>3. Yükleme ve yapılandırma ADAL
Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.  Azure AD ile ADAL toocommunicate için tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.

1. CocoaPods kullanarak ADAL toohello DirectorySearcher proje ekleyerek başlayın.

    ```
    $ vi Podfile
    ```
2. Toothis podfile aşağıdaki hello ekleyin:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Şimdi CocoaPods kullanarak hello podfile dosyasını yükleyin. Bu adım, yüklediğiniz yeni bir XCode çalışma alanı oluşturur.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. Merhaba hızlı başlangıç projesi hello plist dosyasını açın `settings.plist`.  Hello Azure portal girdiğiniz hello bölüm tooreflect hello değerleri hello öğelerinde Hello değerlerini değiştirin. ADAL kullandığında kodunuzu bu değerleri başvurur.
  * Merhaba `tenant` Azure AD kiracınız, örneğin, contoso.onmicrosoft.com hello etki alanıdır.
  * Merhaba `clientId` hello portalından kopyalandığından, uygulamanızın hello istemci kimliği.
  * Merhaba `redirectUri` hello Portalı'nda kayıtlı hello yeniden yönlendirme URL'si.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Azure AD'den ADAL tooget belirteçleri kullanın
Merhaba temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, bu yalnızca bir completionBlock çağırdığı ilkesidir `+(void) getToken : `, ve ADAL rest hello.  

1. Merhaba, `QuickStart` proje, açık `GraphAPICaller.m` ve hello bulun `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` hello üstüne yakın açıklama.  Burada ADAL hello koordinatları CompletionBlock, Azure AD ile toocommunicate aracılığıyla geçirmek ve nasıl söyleyin budur toocache belirteçleri.

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. Şimdi toouse Bu belirteci toosearch hello grafik alanındaki kullanıcılar için ihtiyacımız var. Hello bulur `// TODO: implement SearchUsersList` açıklama. Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir GET isteği toohello Azure AD Graph API tooquery sağlar.  tooquery hello Azure AD grafik API'si, gereksinim duyduğunuz tooinclude bir access_token ile Merhaba `Authorization` hello isteği üstbilgisi. ADAL nereden geldiğini budur.

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

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
         }];

    }

    ```


3. Uygulamanızı isteğinde bulunduğunda bir belirteç çağırarak `getToken(...)`, ADAL tooreturn bir belirteç hello kullanıcı kimlik bilgilerinin sorulmasına olmadan çalışır.  ADAL tooget bir belirteç toosign hello kullanıcı gerektiğini belirlerse, oturum açma için bir iletişim kutusu görüntüler, hello kullanıcının kimlik bilgilerini toplamak ve sonra bir belirteç başarılı kimlik doğrulamasından sonra geri dönüp.  ADAL mümkün tooreturn bir belirteç herhangi bir nedenle değilse oluşturur bir `AdalException`.

> [!Note] 
> Merhaba `AuthenticationResult` nesnesini içeren bir `tokenCacheStoreItem` uygulamanız gerekebilir kullanılan toocollect hello bilgi olabilir nesnesi. Merhaba hızlı başlangıç, içinde `tokenCacheStoreItem` kullanılan toodetermine ise kimlik doğrulaması zaten yapıldı.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Derleme ve Merhaba uygulaması çalıştırma
Tebrikler! Artık çalışan bir iOS uygulama kullanıcıların kimlik doğrulaması, güvenli bir şekilde OAuth 2.0 kullanarak Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri elde var.  Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.  Hızlı Başlangıç uygulamanızı başlatın ve ardından kullanıcılar bir oturum açın.  Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.  Merhaba uygulamayı kapatın ve yeniden başlatın.  Merhaba kullanıcının oturumunu değişmeden kalır dikkat edin.

ADAL kolay tooincorporate kılar uygulamanıza bu ortak kimlik özelliklerin tümü.  Bunu tüm hello dirty çalışmanın sizin için önbellek yönetimi gibi OAuth protokol desteği ile bir kullanıcı Arabirimi toosign hello kullanıcı sunan ve belirteçlerin süresinin yenileme mvc'deki.  Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `getToken`.

Başvuru için üzerinde tamamlandı hello örnek (yapılandırma değerleriniz olmadan) sağlanır [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Sonraki adımlar
Şimdi tooadditional senaryoları taşıyabilirsiniz.  Tootry isteyebilirsiniz:

* [Node.JS Web API'si Azure AD ile güvenli](active-directory-devquickstarts-webapi-nodejs.md)
* Bilgi [nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak iOS](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

