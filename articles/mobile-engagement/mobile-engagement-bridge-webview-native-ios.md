---
title: "Yerel Mobile Engagement iOS SDK'sı ile aaaBridge iOS Web görünümü"
description: "Açıklar nasıl toocreate Javascript ve hello yerel Mobile Engagement iOS SDK'sı çalıştıran Web görünümü arasında bir köprü"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>Yerel Mobile Engagement iOS SDK ile iOS WebView köprüsü
> [!div class="op_single_selector"]
> * [Android köprüsü](mobile-engagement-bridge-webview-native-android.md)
> * [iOS köprüsü](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Bazı mobil uygulamalar, nerede hello uygulamanın kendi yerel iOS Objective-C geliştirme kullanılarak geliştirilen ancak bile tümünü veya bazılarını hello ekranlar WebView iOS içinde işlenir bir karma uygulama olarak tasarlanmıştır. Bu tür uygulamaların içindeki Mobile Engagement iOS SDK'sı hala kullanabilir ve bu öğreticinin açıklar nasıl bunu yapma hakkında toogo. 

Vardır iki yaklaşım tooachieve bu her ikisi de belgelenmemiş ancak:

* Bir bu ilk açıklanan [bağlantı](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) kaydetme içerir bir `UIWebViewDelegate` web görünümü ve catch-ve-hemen-iptal JavaScript'te yapılan bir konum Değiştir. 
* Bir bu ikinci dayanır [WWDC 2013 oturum](https://developer.apple.com/videos/play/wwdc2013/615), olduğu hello temizleyici ilk ve biz bu kılavuzun izleyecek bir yaklaşımdır. Bu yaklaşım yalnızca iOS7 ve üzeri sürümlerde çalıştığını unutmayın. 

Örnek Hello iOS köprülemek için hello adımları izleyin:

1. Öncelikle, aracılığıyla ilerlemiş tooensure gerekir bizim [Başlarken Öğreticisi](mobile-engagement-ios-get-started.md) toointegrate hello karma uygulamanızda Mobile Engagement iOS SDK'sı. İsteğe bağlı olarak, biz hello görünümünden tetiklemek gibi hello SDK yöntemleri görebilmeniz için test gibi günlüğe kaydetmeyi etkinleştirebilirsiniz. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Şimdi karma uygulamanızı bir Web görünümü ekranla olduğundan emin olun. Toohello ekleme `Main.storyboard` hello uygulamasının. 
3. Bu Web görünümü ile ilişkilendirmek, **ViewController** tıklatıp hello webview hello görünüm denetleyicisini Sahne toohello sürükleyerek `ViewController.h` yalnızca hello yerleştirme ekran Düzenle `@interface` satır. 
4. Bunu yaptıktan sonra bir iletişim kutusu için bir ad isteyen açılır. Merhaba ad olarak **webView**. `ViewController.h` Dosya hello aşağıdaki gibi görünmelidir:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Merhaba güncelleştireceğiz `ViewController.m` daha sonra dosya ancak yaygın olarak kullanılan bazı Mobile Engagement iOS SDK yöntemleri bir sarmalayıcı oluşturur hello köprüsü dosyasını ilk oluşturacağız. Adlı yeni bir üst bilgi dosyası oluştur **EngagementJsExports.h** hello kullanan `JSExport` hello daha önce bahsedilen açıklanan mekanizması [oturum](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello yerel iOS yöntemleri. 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. Merhaba köprüsü dosyasının hello ikinci bölümü sonraki oluşturacağız. Adlı bir dosya oluşturun **EngagementJsExports.m** hello Mobile Engagement iOS SDK yöntemlerini çağırarak hello gerçek sarmalayıcıları oluşturma hello uygulama içerecek. Ayrıca biz hello ayrıştırma Not `extras` hello webview JavaScript'ten geçirilen ve, içine koyma bir `NSMutableDictionary` nesne toobe çağrıları hello Engagement SDK'sı yöntemi ile geçirildi.  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. Biz toohello döndürülmesini artık **ViewController.m** ve koddan hello ile güncelleştirin: 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. Not hello aşağıdaki noktaları hello hakkında **ViewController.m** dosyası:
   
   * Merhaba, `loadWebView` yöntemi, biz yüklenirken adlı yerel bir HTML dosyası **LocalPage.html** biz gözden sonraki kodu. 
   * Merhaba, `webViewDidFinishLoad` yöntemi, biz hello kapmasını `JsContext` ve bizim sarmalayıcı sınıfı ile ilişkilendirme. Bu bizim sarmalayıcı hello işleci kullanılarak SDK yöntemleri çağırma sağlayacak **EngagementJs** hello webView gelen. 
9. Adlı bir dosya oluşturun **LocalPage.html** koddan hello ile:
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. Not hello aşağıdaki hello HTML dosyası hakkında yukarıdaki noktaları:
    
    * Burada, olay, iş, hata, appInfo adları olarak kullanılan veri toobe sağlayabilirsiniz giriş kutularının kümesi içerir. Merhaba düğmesine bir sonraki tooit tıklattığınızda toohello sonunda hello yöntemleri bu çağrı toohello Mobile Engagement iOS SDK'sı hello köprüsü dosya toopass çağıran Javascript bir çağrı yapılır. 
    * Bunun nasıl yapılacağı ki bazı statik ek bilgi toohello olayları, işler ve hatta hataları toodemonstrate etiketleme. JSON dize olarak, bu ek bilgileri hello bakarsanız gönderilir `EngagementJsExports.m` dosya, ayrıştırılır ve olaylar, işleri, hataları gönderme birlikte geçirildi. 
    * Mobile Engagement iş için 10 saniye çalıştırın ve bilgisayarı kapat hello giriş kutusunda belirttiğiniz hello adla koparılan. 
    * Mobile Engagement appInfo veya etiketi 'ile customer_name' hello statik anahtar ve hello girişinde hello değeri olarak hello etiketi için girdiğiniz hello değer olarak geçirilir. 
11. Çalışma hello uygulama ve hello aşağıdaki görürsünüz. Şimdi aşağıdaki hello gibi bir test olayı için bazı ad ve tıklatın **Gönder** sonraki tooit. 
    
     ![][1]
12. Toohello giderseniz şimdi **İzleyici** 'ın altına bakın ve uygulama sekmesinde **olayları -> ayrıntıları**, hello statik uygulama biz Gönderen bilgisi birlikte görünmesini bu olay görürsünüz. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
