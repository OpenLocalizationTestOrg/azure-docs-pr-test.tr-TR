---
title: "Azure Notification Hubs ile anında iletme bildirimleri tooiOS aaaSending | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan iOS uygulaması öğrenin."
services: notification-hubs
documentationcenter: ios
keywords: "anında iletme bildirimi,anında iletme bildirimleri,ios anında iletme bildirimleri"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>Azure Notification Hubs ile anında iletme bildirimleri tooiOS gönderme
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).
> 
> 

Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan iOS uygulaması gösterir. Hello kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturacaksınız [Apple anında iletilen bildirim servisi (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.

## <a name="before-you-begin"></a>Başlamadan önce
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Bu öğreticinin tamamlanan hello kodu bulunabilir [github'da](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici hello aşağıdakileri gerektirir:

* [Mobile Services iOS SDK'sı sürüm 1.2.4]
* [Xcode]'un en son sürümü
* iOS 8 (veya sonraki bir sürümü) uyumlu bir cihaz
* [Apple Developer Program](https://developer.apple.com/programs/) üyeliği.
  
  > [!NOTE]
  > Anında iletme bildirimlerinin yapılandırma gereksinimleri nedeniyle, dağıtmak ve hello iOS simülatörü yerine bir fiziksel iOS cihazında (iPhone veya iPad) anında iletme bildirimleri test.
  > 
  > 

Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>iOS anında iletme bildirimleri için Notification Hub'ınızı yapılandırma
Bu bölümde, yeni bir bildirim hub'ı oluşturma ve hello kullanarak APNS ile kimlik doğrulaması yapılandırma açıklanmaktadır **.p12** oluşturduğunuz bildirim sertifikası. Önceden oluşturduğunuz bir bildirim hub'ı toouse istiyorsanız, toostep 5 atlayabilirsiniz.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Merhaba tıklatın <b>Bildirim Hizmetleri</b> hello düğmesini <b>ayarları</b> dikey penceresinde, ardından <b>Apple (APNS)</b>. Tıklayın <b>sertifikasını karşıya yükle</b> ve select hello <b>.p12</b> daha önce dışarı aktarılan dosya. Ayrıca hello doğru parolayı belirttiğinizden emin olun.</p>

<p>Emin tooselect olun <b>korumalı alan</b> bu geliştirme için olduğundan modu. Yalnızca hello kullan <b>üretim</b> uygulamanızı hello mağazadan satın alan toosend anında iletme bildirimleri toousers istiyorsanız.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![Azure portalında APNS yapılandırın](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![Azure Portal'da APNS sertifikası yapılandırma](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

Bildirim hub'ınız şimdi APNS ile yapılandırılmış toowork olan ve hello bağlantı dizeleri tooregister uygulamanızı çalıştırdıktan ve anında iletme bildirimleri göndermek.

## <a name="connect-your-ios-app-toonotification-hubs"></a>İOS uygulama tooNotification hub Bağlan
1. Xcode'da yeni bir iOS projesi oluşturun ve seçin hello **tek görünüm uygulaması** şablonu.
   
    ![Xcode - Single View Application (Tek Görünüm Uygulaması)][8]
    
2. Yeni projeniz için başlangıç seçeneklerini ayarlarken toouse aynı hello emin olun **ürün adı** ve **kuruluş tanımlayıcı** hello paket kimliği daha önce Apple Developer hello üzerinde ayarlarken kullandığınız Portal.
   
    ![Xcode - proje seçenekleri][11]
    
3. Altında **hedefleri**, projenizin adına tıklayın, hello tıklatın **Build Settings** sekmesinde ve genişletin **kod imzalama kimliği**ve ardından **hataayıklama**, kod imzalama kimliğinizi ayarlayın. İki durumlu **düzeyleri** gelen **temel** çok**tüm**ve **sağlama profili** toohello daha önce oluşturduğunuz profili sağlama .
   
    Yeni sağlama Xcode'da oluşturduğunuz profili hello göremiyorsanız imzalama kimliğiniz için hello profilleri yenilemeyi deneyin. ' I tıklatın **Xcode** hello menü çubuğunda **Tercihler**, hello tıklatın **hesap** sekmesini ve ardından hello **ayrıntıları görüntüle** düğmesini tıklatın, kimlik imzalama ve hello hello sağ alt köşedeki Yenile düğmesini tıklatın.
   
    ![Xcode - hazırlama profili][9]
4. Merhaba karşıdan [Mobile Services iOS SDK'sı sürüm 1.2.4] ve hello dosyanın sıkıştırmasını açın. Xcode'da projenize sağ tıklayın ve hello **için dosyaları Ekle** seçeneği tooadd hello **WindowsAzureMessaging.framework** klasörü tooyour Xcode projesi. **Copy items if needed** (Gerekirse öğeleri kopyala) seçeneğini belirleyin ve ardından **Add** (Ekle) seçeneğine tıklayın.
   
   > [!NOTE]
   > Merhaba bildirim hub'ları SDK Xcode 7'de bitcode'u şu anda desteklemiyor.  Ayarlamalısınız **Bitcode'u etkinleştir** çok**Hayır** hello içinde **derleme seçenekleri** projeniz için.
   > 
   > 
   
    ![Azure SDK'nın sıkıştırmasını açma][10]
5. Adlı yeni bir üstbilgi dosyası tooyour proje eklemek `HubInfo.h`. Bu dosya, bildirim hub'ınız için hello sabitleri tutar.  Tanımları aşağıdaki hello ekleyin ve hello ile dize sabiti yer tutucularını değiştirin, *hub adı* ve hello *DefaultListenSharedAccessSignature* daha önce not ettiğiniz.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Açık, `AppDelegate.h` dosyasını içeri aktarma yönergeleri izleyerek hello ekleyin:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. İçinde `AppDelegate.m file`, hello kodda aşağıdaki hello eklemek `didFinishLaunchingWithOptions` yöntemi iOS sürümünüze bağlı. Bu kod, cihaz tanıtıcınızı APNs'ye kaydeder:
   
    iOS 8 için:
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    İOS sürümleri önceki too8 için:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. Aynı dosya Merhaba, yöntemler aşağıdaki hello ekleyin. Bu kod, Hubınfo.h içinde belirttiğiniz hello bağlantı bilgilerini kullanarak toohello bildirim hub'ı bağlar. Merhaba bildirim hub'ı bildirimleri gönderebilmesi hello cihaz belirteci toohello bildirim hub'ı sonra sağlar:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. Buna Merhaba aynı dosya, yöntem toodisplay aşağıdaki hello eklemek bir **Uıalert** hello uygulama etkin durumdayken hello bildirim alınırsa:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Derleme ve hello uygulama hiçbir hatalar varsa, cihaz tooverify üzerinde çalıştırın.

## <a name="send-test-push-notifications"></a>Test amaçlı anında iletme bildirimleri gönderme
Hello anında iletme bildirimleri göndererek uygulamanızda bildirim almayı test edebilirsiniz [Azure Portal] hello aracılığıyla **sorun giderme** hello hub dikey bölümde (Merhaba kullanmak *Test gönderimi* seçeneği).

![Azure Portal - Test Gönderimi][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(İsteğe bağlı) Merhaba uygulamadan anında iletme bildirimleri gönderme
> [!IMPORTANT]
> Bu örneği hello istemci uygulamasından bildirim gönderme sadece öğrenme amaçları için sağlanır. Bu hello gerektirir beri `DefaultFullSharedAccessSignature` toobe hello istemci uygulaması varsa, bir kullanıcının erişim yetkisiz toosend bildirimlerine tooyour istemcileri kazanabilir bildirim hub'ı toohello riskini gösterir.
> 
> 

Bir uygulama içinde toosend anında iletme bildirimleri istiyorsanız, bu bölümde nasıl bir örnek sağlar toodo hello REST arabirimini kullanarak bu.

1. Xcode'da, açık `Main.storyboard` ve hello Nesne Kitaplığı tooallow hello kullanıcı toosend anında iletme bildirimleri hello uygulama kullanıcı Arabirimi bileşenlerini yükseltmesinin hello ekleyin:
   
   * Etiket metni olmayan bir etiket. Bildirimleri gönderirken kullanılan tooreport hataları olacaktır. Merhaba **satırları** özelliği çok ayarlanmalıdır**0** böylece kısıtlanmış toohello sağ ve sol kenar boşluklarına ve hello üst hello görünümün otomatik olarak boyutlandırılır.
   * Bir metin alanı **yer tutucu** metin ayarlamak çok**bildirim iletisi girin**. Aşağıda gösterildiği gibi yalnızca hello etiket altındaki Hello alanı kısıtlar. Merhaba View Controller hello çıkış temsilcisi olarak ayarlayın.
   * Adlı bir düğme **bildirim gönder** hemen hello metin alanı altında ve hello yatay ortada kısıtlanmış.
     
     Merhaba görünüm aşağıdaki gibi görünmelidir:
     
     ![Xcode tasarımcısı][32]
2. [Çıkışlar ekleyin](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) hello etiket ve metin alanı görünümünüze bağlı için ve güncelleştirme, `interface` tanımı toosupport `UITextFieldDelegate` ve `NSXMLParserDelegate`. Merhaba Hello REST API çağırma ve hello yanıt ayrıştırmayı toohelp desteği gösterilen üç özellik bildirimini ekleyin.
   
    ViewController.h dosyanız aşağıdaki gibi görünmelidir:
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Açık `HubInfo.h` ve bildirimleri tooyour hub göndermek için kullanılacak olan sabitleri aşağıdaki hello ekleyin. Merhaba yer tutucu dize sabitini, gerçek Değiştir *DefaultFullSharedAccessSignature* bağlantı dizesi.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Merhaba aşağıdakileri ekleyin `#import` deyimleri tooyour `ViewController.h` dosya.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. İçinde `ViewController.m` kod toohello arabirim uygulamasına aşağıdaki hello ekleyin. Bu kod, *DefaultFullSharedAccessSignature* bağlantı dizenizi ayrıştırır. Hello belirtildiği gibi [REST API Başvurusu](http://msdn.microsoft.com/library/azure/dn495627.aspx), bu ayrıştırılmış bilgiler kullanılan toogenerate hello için bir SaS belirteci olacaktır **yetkilendirme** istek üstbilgisi.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. İçinde `ViewController.m`, güncelleştirme hello `viewDidLoad` hello görünüm yüklenirken yöntemi tooparse hello bağlantı dizesi. Ayrıca, aşağıda gösterilen hello yardımcı program yöntemlerini ekleyin toohello arabirim uygulaması.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. İçinde `ViewController.m`, hello sağlanan kod toohello arabirimi uygulama toogenerate hello SaS yetkilendirme belirtecini aşağıdaki hello eklemek **yetkilendirme** hello belirtildiği gibi üst [REST API'si Başvuru](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. CTRL + Sürükle gelen hello **bildirim gönder** çok düğmesini`ViewController.m` tooadd adlı bir eylem **SendNotificationMessage** hello için **Touch Down** olay. Kod toosend hello bildirim hello REST API kullanarak aşağıdaki hello ile yöntemi güncelleştirin.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. İçinde `ViewController.m`, aşağıdaki temsilci yöntemini toosupport hello metin alanı için hello klavye kapatmayı hello ekleyin. CTRL + Sürükle simgesinden hello metin alanı toohello View Controller hello arabirimi Tasarımcı tooset hello denetleyicisi hello çıkış temsilcisi olarak görüntüleyin.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. İçinde `ViewController.m`, hello aşağıdaki temsilci yöntemlerini toosupport ayrıştırma hello yanıt kullanarak eklemek `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Merhaba projeyi oluşturun ve hiçbir hata doğrulayın.

> [!NOTE]
> Xcode7 bitcode'u desteği hakkında bir derleme hatası karşılaşırsanız hello değiştirmelisiniz **Build Settings** > **etkinleştirmek Bitcode (enable_bıtcode)** çok**Hayır** Xcode'da. Merhaba Notification Hubs SDK'sı şu anda bitcode'u desteklemiyor. 
> 
> 

Merhaba Apple tüm hello olası bildirim yüklerini bulabilirsiniz [yerel ve anında iletilen bildirim Programlama Kılavuzu].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Uygulamanızın anında iletme bildirimleri alıp almadığını denetleme
tootest anında iletme bildirimlerini iOS hello uygulama tooa fiziksel iOS cihazına dağıtmanız gerekir. Merhaba iOS simülatörü'nü kullanarak Apple anında iletme bildirimleri gönderemezsiniz.

1. Merhaba uygulamayı çalıştırın ve kayıt başarılı tuşuna basarak olduğunu doğrulayın ve **Tamam**.
   
    ![iOS Uygulaması Anında İletme Bildirimi Kayıt Testi][33]
2. Merhaba bir sınama anında iletme bildirimi gönderebilirsiniz [Azure Portal], yukarıda açıklandığı gibi. Hello uygulamasında anında iletme bildirimleri göndermek için kod eklediyseniz, bir bildirim iletisi hello metin alanı tooenter dokunun. Hello tuşuna **Gönder** hello klavye veya hello düğmesine **bildirim gönder** hello görünüm toosend hello bildirim iletisi düğmesini.
   
    ![iOS Uygulaması Anında İletilen Bildirim Gönderme Testi][34]
3. Merhaba anında iletme bildirimi kayıtlı tooreceive hello bildirimleri tooall cihazlara gönderilen belirli bildirim Hub'hello.
   
    ![iOS Uygulaması Anında İletilen Bildirim Alma Testi][35]

## <a name="next-steps"></a>Sonraki adımlar
Bu basit örnekte, kayıtlı iOS cihazlarınıza anında iletme bildirimleri tooall yayımladınız. Toohello devam öğrendiklerinizi bir sonraki adım olarak önerdiğimiz [Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile iOS için] öğretici, bir arka uç toosend anında iletme bildirimleri etiketleri kullanarak oluşturmada size yol gösterir. 

Kullanıcılarınızı ilgi alanı gruplarına göre toosegment isterseniz, ayrıca toohello üzerinde taşıyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend] Öğreticisi. 

Notification Hubs hakkında genel bilgi için bkz. [Notification Hubs Kılavuzu].

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[Mobile Services iOS SDK'sı sürüm 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile iOS için]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[yerel ve anında iletilen bildirim Programlama Kılavuzu]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
