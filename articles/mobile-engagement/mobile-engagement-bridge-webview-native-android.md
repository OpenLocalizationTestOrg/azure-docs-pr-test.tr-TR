---
title: "aaaBridge yerel Mobile Engagement Android SDK'sı Android WebView"
description: "Açıklar nasıl toocreate WebView arasında bir köprü Javascript çalıştıran ve yerel Mobile Engagement Android SDK hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="a6302-103">Yerel Mobile Engagement Android SDK'sı Android WebView köprüsü</span><span class="sxs-lookup"><span data-stu-id="a6302-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6302-104">Android köprüsü</span><span class="sxs-lookup"><span data-stu-id="a6302-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="a6302-105">iOS köprüsü</span><span class="sxs-lookup"><span data-stu-id="a6302-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="a6302-106">Bazı mobil uygulamalar, nerede hello uygulamanın kendi yerel Android geliştirme kullanılarak geliştirilen ancak hello ekranlar bile tümünün veya bir Android WebView içinde işlenir bir karma uygulama olarak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a6302-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="a6302-107">Mobile Engagement Android SDK içinde bu tür uygulamalar hala kullanabilir ve bu öğreticinin açıklar nasıl bunu yapma hakkında toogo.</span><span class="sxs-lookup"><span data-stu-id="a6302-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="a6302-108">Aşağıdaki Hello örnek kodu Android belgelerine hello üzerinde temel [burada](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="a6302-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="a6302-109">Bu belgelenen yaklaşım nasıl kullanılabilecek açıklar tooimplement Merhaba, aynı, karma uygulama görünümünden de istekleri tootrack olayları, işler, hatalar, app-info aracılığıyla cmdlet'ine sırasında başlatabilirsiniz, Mobile Engagement Android SDK'ın yöntemleri yaygın olarak kullanılan için Bizim Android SDK.</span><span class="sxs-lookup"><span data-stu-id="a6302-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="a6302-110">Öncelikle, aracılığıyla ilerlemiş tooensure gerekir bizim [Başlarken Öğreticisi](mobile-engagement-android-get-started.md) karma uygulamanızda toointegrate hello Mobile Engagement Android SDK.</span><span class="sxs-lookup"><span data-stu-id="a6302-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="a6302-111">Bunu yaptığınızda, `OnCreate` yöntemi hello aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="a6302-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="a6302-112">Şimdi karma uygulamanızı bir Web görünümü ekranla olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a6302-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="a6302-113">Hello için bu kodu benzer toohello aşağıdaki burada biz yerel bir HTML dosyası yüklenen olacaktır **örnek.HTML** hello hello Webview içinde `onCreate` ekranınızın yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a6302-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="a6302-114">Şimdi adlı bir köprü dosyası oluşturun **WebAppInterface** Mobile Engagement Android SDK yöntemlerini hello kullanarak bir sarmalayıcı bazı yaygın olarak oluşturan kullanılan `@JavascriptInterface` hello açıklanan yaklaşım [Android belgeleri ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="a6302-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="a6302-115">Biz köprüsü dosya yukarıda hello oluşturduktan sonra bizim Webview ile ilişkili olduğunu tooensure ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="a6302-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="a6302-116">Bu toohappen için tooedit gerekir, `SetWebview` yöntemi şekilde hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="a6302-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="a6302-117">Yukarıdaki kod parçacığında Hello biz adlı `addJavascriptInterface` tooassociate bizim köprüsü sınıfı ile bizim Webview ve ayrıca adlı bir tanıtıcı oluşturulan **EngagementJs** hello köprüsü dosyasından toocall hello yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="a6302-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="a6302-118">Şimdi aşağıdaki adlı dosyasına hello oluşturmak **örnek.HTML** projenize bir klasör olarak adlandırılan **varlıklar** Webview hello yüklenir ve burada çağrılacak hello yöntemleri hello köprüsü dosyasından.</span><span class="sxs-lookup"><span data-stu-id="a6302-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="a6302-119">Not hello aşağıdaki hello HTML dosyası hakkında yukarıdaki noktaları:</span><span class="sxs-lookup"><span data-stu-id="a6302-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="a6302-120">Burada, olay, iş, hata, appInfo adları olarak kullanılan veri toobe sağlayabilirsiniz giriş kutularının kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="a6302-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="a6302-121">Merhaba düğmesine bir sonraki tooit tıklattığınızda toohello sonunda hello yöntemleri bu çağrı toohello Mobile Engagement Android SDK hello köprüsü dosya toopass çağıran Javascript bir çağrı yapılır.</span><span class="sxs-lookup"><span data-stu-id="a6302-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="a6302-122">Bunun nasıl yapılacağı ki bazı statik ek bilgi toohello olayları, işler ve hatta hataları toodemonstrate etiketleme.</span><span class="sxs-lookup"><span data-stu-id="a6302-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="a6302-123">JSON dize olarak, bu ek bilgileri hello bakarsanız gönderilir `WebAppInterface` dosya, ayrıştırılır ve bir Android put `Bundle` ve olaylar, işleri, hataları gönderme birlikte geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a6302-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="a6302-124">Mobile Engagement iş için 10 saniye çalıştırın ve bilgisayarı kapat hello giriş kutusunda belirttiğiniz hello adla koparılan.</span><span class="sxs-lookup"><span data-stu-id="a6302-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="a6302-125">Mobile Engagement appInfo veya etiketi 'ile customer_name' hello statik anahtar ve hello girişinde hello değeri olarak hello etiketi için girdiğiniz hello değer olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a6302-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="a6302-126">Çalışma hello uygulama ve hello aşağıdaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a6302-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="a6302-127">Şimdi aşağıdaki hello gibi bir test olayı için bazı ad ve tıklatın **Gönder** altındaki.</span><span class="sxs-lookup"><span data-stu-id="a6302-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="a6302-128">Toohello giderseniz şimdi **İzleyici** 'ın altına bakın ve uygulama sekmesinde **olayları -> ayrıntıları**, hello statik uygulama biz Gönderen bilgisi birlikte görünmesini bu olay görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a6302-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
