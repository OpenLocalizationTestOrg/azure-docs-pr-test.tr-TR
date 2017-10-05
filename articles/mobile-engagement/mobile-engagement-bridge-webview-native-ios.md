---
title: "Yerel Mobile Engagement iOS SDK ile iOS WebView köprüsü"
description: "Javascript ve yerel Mobile Engagement iOS SDK'sı çalıştıran Web görünümü arasında bir köprü oluşturmayı açıklar"
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
ms.openlocfilehash: 35f7bdbeb480122513ae2a0b04a6d8cfd426802a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="88fc3-103">Yerel Mobile Engagement iOS SDK ile iOS WebView köprüsü</span><span class="sxs-lookup"><span data-stu-id="88fc3-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="88fc3-104">Android köprüsü</span><span class="sxs-lookup"><span data-stu-id="88fc3-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="88fc3-105">iOS köprüsü</span><span class="sxs-lookup"><span data-stu-id="88fc3-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="88fc3-106">Bazı mobil uygulamalar, uygulamanın kendi yerel iOS Objective-C geliştirme kullanılarak geliştirilen ancak bile tümünü veya bazılarını ekranlar WebView iOS içinde işlenir bir karma uygulama olarak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="88fc3-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native iOS Objective-C development but some or even all of the screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="88fc3-107">Bu tür uygulamaların içindeki Mobile Engagement iOS SDK'sı hala tüketebileceği ve Bu öğreticide bunu yapma hakkında Git açıklar.</span><span class="sxs-lookup"><span data-stu-id="88fc3-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how to go about doing this.</span></span> 

<span data-ttu-id="88fc3-108">Her ikisi de belgelenmemiş ancak bunun için iki yaklaşım vardır:</span><span class="sxs-lookup"><span data-stu-id="88fc3-108">There are two approaches to achieve this though both are undocumented:</span></span>

* <span data-ttu-id="88fc3-109">Bir bu ilk açıklanan [bağlantı](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) kaydetme içerir bir `UIWebViewDelegate` web görünümü ve catch-ve-hemen-iptal JavaScript'te yapılan bir konum Değiştir.</span><span class="sxs-lookup"><span data-stu-id="88fc3-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="88fc3-110">Bir bu ikinci dayanır [WWDC 2013 oturum](https://developer.apple.com/videos/play/wwdc2013/615), ilk temizleyici olduğu ve biz bu kılavuzun izleyecek bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="88fc3-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than the first and which we will follow for this guide.</span></span> <span data-ttu-id="88fc3-111">Bu yaklaşım yalnızca iOS7 ve üzeri sürümlerde çalıştığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="88fc3-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="88fc3-112">Örnek iOS köprülemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="88fc3-112">Follow the steps below for the iOS bridge sample:</span></span>

1. <span data-ttu-id="88fc3-113">Öncelikle, çalıştınız emin olmak gereken bizim [Başlarken Öğreticisi](mobile-engagement-ios-get-started.md) karma uygulamanızı Mobile Engagement iOS SDK'sını tümleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="88fc3-113">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) to integrate the Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="88fc3-114">İsteğe bağlı olarak, biz görünümünden tetiklemek gibi SDK yöntemleri görebilmeniz için test gibi günlüğe kaydetmeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88fc3-114">Optionally, you can also enable test logging as follows so that you can see the SDK methods as we trigger them from the webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="88fc3-115">Şimdi karma uygulamanızı bir Web görünümü ekranla olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88fc3-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="88fc3-116">Ona ekleyebilirsiniz `Main.storyboard` uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="88fc3-116">You can add it to the `Main.storyboard` of the app.</span></span> 
3. <span data-ttu-id="88fc3-117">Bu Web görünümü ile ilişkilendirmek, **ViewController** tıklatıp Görünüm denetleyicisini Sahne gelen webview sürükleyerek `ViewController.h` yerleştirerek ekran Düzenle yalnızca aşağıda `@interface` satır.</span><span class="sxs-lookup"><span data-stu-id="88fc3-117">Associate this webview with your **ViewController** by clicking and dragging the webview from the View Controller Scene to the `ViewController.h` edit screen, placing it just below the `@interface` line.</span></span> 
4. <span data-ttu-id="88fc3-118">Bunu yaptıktan sonra bir iletişim kutusu için bir ad isteyen açılır.</span><span class="sxs-lookup"><span data-stu-id="88fc3-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="88fc3-119">Ad olarak **webView**.</span><span class="sxs-lookup"><span data-stu-id="88fc3-119">Provide the name as **webView**.</span></span> <span data-ttu-id="88fc3-120">`ViewController.h` Dosya, aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="88fc3-120">Your `ViewController.h` file should look like the following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="88fc3-121">Güncelleştireceğiz `ViewController.m` daha sonra dosya ancak yaygın olarak kullanılan bazı Mobile Engagement iOS SDK yöntemleri bir sarmalayıcı oluşturur köprüsü dosyasının ilk oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="88fc3-121">We will update the `ViewController.m` file later but first we will create the bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="88fc3-122">Adlı yeni bir üst bilgi dosyası oluştur **EngagementJsExports.h** kullanan `JSExport` daha önce bahsedilen içinde açıklanan mekanizması [oturum](https://developer.apple.com/videos/play/wwdc2013/615) yerel iOS yöntemleri göstermek için.</span><span class="sxs-lookup"><span data-stu-id="88fc3-122">Create a new header file called **EngagementJsExports.h** which uses the `JSExport` mechanism described in the aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) to expose the native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="88fc3-123">Sonraki ikinci bölümü köprüsü dosyasının oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="88fc3-123">Next we will create the second part of the bridge file.</span></span> <span data-ttu-id="88fc3-124">Adlı bir dosya oluşturun **EngagementJsExports.m** Mobile Engagement iOS SDK yöntemlerini çağırarak gerçek sarmalayıcıları oluşturma uygulama içerecek.</span><span class="sxs-lookup"><span data-stu-id="88fc3-124">Create a file called **EngagementJsExports.m** which will contain the implementation creating the actual wrappers by calling the Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="88fc3-125">Ayrıca biz ayrıştırma Not `extras` webview JavaScript'ten geçirilen ve, içine koyma bir `NSMutableDictionary` ile Engagement SDK'sı yöntem çağrılarını geçirilecek nesnesi.</span><span class="sxs-lookup"><span data-stu-id="88fc3-125">Also note that we are parsing the `extras` being passed from the webview javascript and putting that into an `NSMutableDictionary` object to be passed with the Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="88fc3-126">Biz geri gelmeniz artık **ViewController.m** ve aşağıdaki kod ile güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="88fc3-126">Now we come back to the **ViewController.m** and update it with the following code:</span></span> 
   
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
8. <span data-ttu-id="88fc3-127">İlgili aşağıdaki noktalara dikkat edin **ViewController.m** dosyası:</span><span class="sxs-lookup"><span data-stu-id="88fc3-127">Note the following points about the **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="88fc3-128">İçinde `loadWebView` yöntemi, biz yüklenirken adlı yerel bir HTML dosyası **LocalPage.html** biz gözden sonraki kodu.</span><span class="sxs-lookup"><span data-stu-id="88fc3-128">In the `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="88fc3-129">İçinde `webViewDidFinishLoad` yöntemi, biz ele geçirme `JsContext` ve bizim sarmalayıcı sınıfı ile ilişkilendirme.</span><span class="sxs-lookup"><span data-stu-id="88fc3-129">In the `webViewDidFinishLoad` method, we are grabbing the `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="88fc3-130">Bu bizim sarmalayıcı işleci kullanılarak SDK yöntemleri çağırma sağlayacak **EngagementJs** webView gelen.</span><span class="sxs-lookup"><span data-stu-id="88fc3-130">This will allow calling our wrapper SDK methods using the handle **EngagementJs** from the webView.</span></span> 
9. <span data-ttu-id="88fc3-131">Adlı bir dosya oluşturun **LocalPage.html** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="88fc3-131">Create a file called **LocalPage.html** with the following code:</span></span>
   
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
                       // Example of how extras info can be passed with the Engagement logs
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
10. <span data-ttu-id="88fc3-132">Yukarıdaki HTML dosya ile ilgili aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="88fc3-132">Note the following points about the HTML file above:</span></span>
    
    * <span data-ttu-id="88fc3-133">Olay, iş, hata, appInfo adları olarak kullanılacak verileri nerede sağlayabilir giriş kutularının kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="88fc3-133">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="88fc3-134">Yanında düğmesine tıkladığınızda sonuçta Mobile Engagement iOS SDK'sı bu çağrıyı geçirmek için köprü dosyasından yöntemlerini çağıran Javascript için bir çağrı yapılır.</span><span class="sxs-lookup"><span data-stu-id="88fc3-134">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="88fc3-135">Olaylar, işler ve bu nasıl yapılabilir göstermek için bile hatalar için statik bazı ek bilgiler üzerinde etiketleme.</span><span class="sxs-lookup"><span data-stu-id="88fc3-135">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="88fc3-136">Bakarsanız JSON dize olarak, bu ek bilgileri gönderilir `EngagementJsExports.m` dosya, ayrıştırılır ve olaylar, işleri, hataları gönderme birlikte geçirildi.</span><span class="sxs-lookup"><span data-stu-id="88fc3-136">This extra info is sent as a JSON string which, if you look in the `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="88fc3-137">Mobile Engagement işi için 10 saniye çalıştırın ve bilgisayarı kapat giriş kutusunda belirttiğiniz adla koparılan.</span><span class="sxs-lookup"><span data-stu-id="88fc3-137">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="88fc3-138">Mobile Engagement appInfo veya etiketi statik anahtarı ve değeri olarak giriş etiketi için girilen değer olarak 'customer_name' ile geçirilir.</span><span class="sxs-lookup"><span data-stu-id="88fc3-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
11. <span data-ttu-id="88fc3-139">Uygulamayı çalıştırın ve aşağıdaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="88fc3-139">Run the app and you will see the following.</span></span> <span data-ttu-id="88fc3-140">Şimdi aşağıdaki gibi bir test olayı için bazı ad ve tıklatın **Gönder** yanında.</span><span class="sxs-lookup"><span data-stu-id="88fc3-140">Now provide some name for a test event like the following and click **Send** next to it.</span></span> 
    
     ![][1]
12. <span data-ttu-id="88fc3-141">Giderseniz şimdi **İzleyici** 'ın altına bakın ve uygulama sekmesinde **olayları -> ayrıntıları**, statik uygulama biz Gönderen bilgisi birlikte görünmesini bu olay görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="88fc3-141">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
