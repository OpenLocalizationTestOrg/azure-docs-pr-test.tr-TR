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
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="6d159-103">Yerel Mobile Engagement iOS SDK ile iOS WebView köprüsü</span><span class="sxs-lookup"><span data-stu-id="6d159-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d159-104">Android köprüsü</span><span class="sxs-lookup"><span data-stu-id="6d159-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="6d159-105">iOS köprüsü</span><span class="sxs-lookup"><span data-stu-id="6d159-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="6d159-106">Bazı mobil uygulamalar, nerede hello uygulamanın kendi yerel iOS Objective-C geliştirme kullanılarak geliştirilen ancak bile tümünü veya bazılarını hello ekranlar WebView iOS içinde işlenir bir karma uygulama olarak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6d159-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="6d159-107">Bu tür uygulamaların içindeki Mobile Engagement iOS SDK'sı hala kullanabilir ve bu öğreticinin açıklar nasıl bunu yapma hakkında toogo.</span><span class="sxs-lookup"><span data-stu-id="6d159-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="6d159-108">Vardır iki yaklaşım tooachieve bu her ikisi de belgelenmemiş ancak:</span><span class="sxs-lookup"><span data-stu-id="6d159-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="6d159-109">Bir bu ilk açıklanan [bağlantı](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) kaydetme içerir bir `UIWebViewDelegate` web görünümü ve catch-ve-hemen-iptal JavaScript'te yapılan bir konum Değiştir.</span><span class="sxs-lookup"><span data-stu-id="6d159-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="6d159-110">Bir bu ikinci dayanır [WWDC 2013 oturum](https://developer.apple.com/videos/play/wwdc2013/615), olduğu hello temizleyici ilk ve biz bu kılavuzun izleyecek bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="6d159-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="6d159-111">Bu yaklaşım yalnızca iOS7 ve üzeri sürümlerde çalıştığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6d159-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="6d159-112">Örnek Hello iOS köprülemek için hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d159-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="6d159-113">Öncelikle, aracılığıyla ilerlemiş tooensure gerekir bizim [Başlarken Öğreticisi](mobile-engagement-ios-get-started.md) toointegrate hello karma uygulamanızda Mobile Engagement iOS SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="6d159-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="6d159-114">İsteğe bağlı olarak, biz hello görünümünden tetiklemek gibi hello SDK yöntemleri görebilmeniz için test gibi günlüğe kaydetmeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d159-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="6d159-115">Şimdi karma uygulamanızı bir Web görünümü ekranla olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6d159-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="6d159-116">Toohello ekleme `Main.storyboard` hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="6d159-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="6d159-117">Bu Web görünümü ile ilişkilendirmek, **ViewController** tıklatıp hello webview hello görünüm denetleyicisini Sahne toohello sürükleyerek `ViewController.h` yalnızca hello yerleştirme ekran Düzenle `@interface` satır.</span><span class="sxs-lookup"><span data-stu-id="6d159-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="6d159-118">Bunu yaptıktan sonra bir iletişim kutusu için bir ad isteyen açılır.</span><span class="sxs-lookup"><span data-stu-id="6d159-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="6d159-119">Merhaba ad olarak **webView**.</span><span class="sxs-lookup"><span data-stu-id="6d159-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="6d159-120">`ViewController.h` Dosya hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="6d159-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="6d159-121">Merhaba güncelleştireceğiz `ViewController.m` daha sonra dosya ancak yaygın olarak kullanılan bazı Mobile Engagement iOS SDK yöntemleri bir sarmalayıcı oluşturur hello köprüsü dosyasını ilk oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="6d159-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="6d159-122">Adlı yeni bir üst bilgi dosyası oluştur **EngagementJsExports.h** hello kullanan `JSExport` hello daha önce bahsedilen açıklanan mekanizması [oturum](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello yerel iOS yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="6d159-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="6d159-123">Merhaba köprüsü dosyasının hello ikinci bölümü sonraki oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="6d159-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="6d159-124">Adlı bir dosya oluşturun **EngagementJsExports.m** hello Mobile Engagement iOS SDK yöntemlerini çağırarak hello gerçek sarmalayıcıları oluşturma hello uygulama içerecek.</span><span class="sxs-lookup"><span data-stu-id="6d159-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="6d159-125">Ayrıca biz hello ayrıştırma Not `extras` hello webview JavaScript'ten geçirilen ve, içine koyma bir `NSMutableDictionary` nesne toobe çağrıları hello Engagement SDK'sı yöntemi ile geçirildi.</span><span class="sxs-lookup"><span data-stu-id="6d159-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="6d159-126">Biz toohello döndürülmesini artık **ViewController.m** ve koddan hello ile güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="6d159-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="6d159-127">Not hello aşağıdaki noktaları hello hakkında **ViewController.m** dosyası:</span><span class="sxs-lookup"><span data-stu-id="6d159-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="6d159-128">Merhaba, `loadWebView` yöntemi, biz yüklenirken adlı yerel bir HTML dosyası **LocalPage.html** biz gözden sonraki kodu.</span><span class="sxs-lookup"><span data-stu-id="6d159-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="6d159-129">Merhaba, `webViewDidFinishLoad` yöntemi, biz hello kapmasını `JsContext` ve bizim sarmalayıcı sınıfı ile ilişkilendirme.</span><span class="sxs-lookup"><span data-stu-id="6d159-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="6d159-130">Bu bizim sarmalayıcı hello işleci kullanılarak SDK yöntemleri çağırma sağlayacak **EngagementJs** hello webView gelen.</span><span class="sxs-lookup"><span data-stu-id="6d159-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="6d159-131">Adlı bir dosya oluşturun **LocalPage.html** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="6d159-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
10. <span data-ttu-id="6d159-132">Not hello aşağıdaki hello HTML dosyası hakkında yukarıdaki noktaları:</span><span class="sxs-lookup"><span data-stu-id="6d159-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="6d159-133">Burada, olay, iş, hata, appInfo adları olarak kullanılan veri toobe sağlayabilirsiniz giriş kutularının kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="6d159-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="6d159-134">Merhaba düğmesine bir sonraki tooit tıklattığınızda toohello sonunda hello yöntemleri bu çağrı toohello Mobile Engagement iOS SDK'sı hello köprüsü dosya toopass çağıran Javascript bir çağrı yapılır.</span><span class="sxs-lookup"><span data-stu-id="6d159-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="6d159-135">Bunun nasıl yapılacağı ki bazı statik ek bilgi toohello olayları, işler ve hatta hataları toodemonstrate etiketleme.</span><span class="sxs-lookup"><span data-stu-id="6d159-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="6d159-136">JSON dize olarak, bu ek bilgileri hello bakarsanız gönderilir `EngagementJsExports.m` dosya, ayrıştırılır ve olaylar, işleri, hataları gönderme birlikte geçirildi.</span><span class="sxs-lookup"><span data-stu-id="6d159-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="6d159-137">Mobile Engagement iş için 10 saniye çalıştırın ve bilgisayarı kapat hello giriş kutusunda belirttiğiniz hello adla koparılan.</span><span class="sxs-lookup"><span data-stu-id="6d159-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="6d159-138">Mobile Engagement appInfo veya etiketi 'ile customer_name' hello statik anahtar ve hello girişinde hello değeri olarak hello etiketi için girdiğiniz hello değer olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="6d159-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="6d159-139">Çalışma hello uygulama ve hello aşağıdaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6d159-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="6d159-140">Şimdi aşağıdaki hello gibi bir test olayı için bazı ad ve tıklatın **Gönder** sonraki tooit.</span><span class="sxs-lookup"><span data-stu-id="6d159-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="6d159-141">Toohello giderseniz şimdi **İzleyici** 'ın altına bakın ve uygulama sekmesinde **olayları -> ayrıntıları**, hello statik uygulama biz Gönderen bilgisi birlikte görünmesini bu olay görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6d159-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
