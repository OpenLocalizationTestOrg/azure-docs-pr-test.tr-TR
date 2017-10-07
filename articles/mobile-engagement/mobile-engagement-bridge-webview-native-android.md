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
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>Yerel Mobile Engagement Android SDK'sı Android WebView köprüsü
> [!div class="op_single_selector"]
> * [Android köprüsü](mobile-engagement-bridge-webview-native-android.md)
> * [iOS köprüsü](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Bazı mobil uygulamalar, nerede hello uygulamanın kendi yerel Android geliştirme kullanılarak geliştirilen ancak hello ekranlar bile tümünün veya bir Android WebView içinde işlenir bir karma uygulama olarak tasarlanmıştır. Mobile Engagement Android SDK içinde bu tür uygulamalar hala kullanabilir ve bu öğreticinin açıklar nasıl bunu yapma hakkında toogo. Aşağıdaki Hello örnek kodu Android belgelerine hello üzerinde temel [burada](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript). Bu belgelenen yaklaşım nasıl kullanılabilecek açıklar tooimplement Merhaba, aynı, karma uygulama görünümünden de istekleri tootrack olayları, işler, hatalar, app-info aracılığıyla cmdlet'ine sırasında başlatabilirsiniz, Mobile Engagement Android SDK'ın yöntemleri yaygın olarak kullanılan için Bizim Android SDK. 

1. Öncelikle, aracılığıyla ilerlemiş tooensure gerekir bizim [Başlarken Öğreticisi](mobile-engagement-android-get-started.md) karma uygulamanızda toointegrate hello Mobile Engagement Android SDK. Bunu yaptığınızda, `OnCreate` yöntemi hello aşağıdaki gibi görünür.  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. Şimdi karma uygulamanızı bir Web görünümü ekranla olduğundan emin olun. Hello için bu kodu benzer toohello aşağıdaki burada biz yerel bir HTML dosyası yüklenen olacaktır **örnek.HTML** hello hello Webview içinde `onCreate` ekranınızın yöntemi. 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. Şimdi adlı bir köprü dosyası oluşturun **WebAppInterface** Mobile Engagement Android SDK yöntemlerini hello kullanarak bir sarmalayıcı bazı yaygın olarak oluşturan kullanılan `@JavascriptInterface` hello açıklanan yaklaşım [Android belgeleri ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
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
4. Biz köprüsü dosya yukarıda hello oluşturduktan sonra bizim Webview ile ilişkili olduğunu tooensure ihtiyacımız var. Bu toohappen için tooedit gerekir, `SetWebview` yöntemi şekilde hello aşağıdaki gibi görünür:
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. Yukarıdaki kod parçacığında Hello biz adlı `addJavascriptInterface` tooassociate bizim köprüsü sınıfı ile bizim Webview ve ayrıca adlı bir tanıtıcı oluşturulan **EngagementJs** hello köprüsü dosyasından toocall hello yöntemleri. 
6. Şimdi aşağıdaki adlı dosyasına hello oluşturmak **örnek.HTML** projenize bir klasör olarak adlandırılan **varlıklar** Webview hello yüklenir ve burada çağrılacak hello yöntemleri hello köprüsü dosyasından.
   
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
7. Not hello aşağıdaki hello HTML dosyası hakkında yukarıdaki noktaları:
   
   * Burada, olay, iş, hata, appInfo adları olarak kullanılan veri toobe sağlayabilirsiniz giriş kutularının kümesi içerir. Merhaba düğmesine bir sonraki tooit tıklattığınızda toohello sonunda hello yöntemleri bu çağrı toohello Mobile Engagement Android SDK hello köprüsü dosya toopass çağıran Javascript bir çağrı yapılır. 
   * Bunun nasıl yapılacağı ki bazı statik ek bilgi toohello olayları, işler ve hatta hataları toodemonstrate etiketleme. JSON dize olarak, bu ek bilgileri hello bakarsanız gönderilir `WebAppInterface` dosya, ayrıştırılır ve bir Android put `Bundle` ve olaylar, işleri, hataları gönderme birlikte geçirilir. 
   * Mobile Engagement iş için 10 saniye çalıştırın ve bilgisayarı kapat hello giriş kutusunda belirttiğiniz hello adla koparılan. 
   * Mobile Engagement appInfo veya etiketi 'ile customer_name' hello statik anahtar ve hello girişinde hello değeri olarak hello etiketi için girdiğiniz hello değer olarak geçirilir. 
8. Çalışma hello uygulama ve hello aşağıdaki görürsünüz. Şimdi aşağıdaki hello gibi bir test olayı için bazı ad ve tıklatın **Gönder** altındaki. 
   
    ![][1]
9. Toohello giderseniz şimdi **İzleyici** 'ın altına bakın ve uygulama sekmesinde **olayları -> ayrıntıları**, hello statik uygulama biz Gönderen bilgisi birlikte görünmesini bu olay görürsünüz. 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
