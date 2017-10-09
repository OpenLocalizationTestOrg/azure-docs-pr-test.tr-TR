---
title: "Güvenli anında iletme bildirimleri Azure Notification Hubs ile aaaSending"
description: "Nasıl toosend güvenli anında iletme bildirimleri tooan Android uygulaması Azure'dan öğrenin. Java ve C# içinde yazılan kod örnekleri."
documentationcenter: android
keywords: "anında iletme bildirimi, anında iletme bildirimleri, anında iletileri, android anında iletme bildirimleri"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Azure Notification Hubs ile güvenli anında iletme bildirimleri gönderme
> [!div class="op_single_selector"]
> * [Windows Evrensel](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Genel Bakış
> [!IMPORTANT]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Microsoft Azure anında iletme bildirimi desteği tooaccess tüketici ve kurumsal uygulamalar için anında iletme bildirimlerinin hello uyarlamasını büyük ölçüde basitleştirir kullanımı kolay, çok platformlu, ölçeği anında iletme iletisi altyapısı sağlar Mobil platformlar.

Tooregulatory veya güvenlik kısıtlamaları, bazen bir uygulama bir şey hello standart anında iletme bildirimi altyapısı iletilen hello bildirim tooinclude isteyebilirsiniz. Bu öğretici nasıl tooachieve hello aynı deneyimi hello istemci Android cihazı ve hello uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı üzerinden hassas bilgileri göndererek açıklar.

Yüksek bir düzeyde hello akışı aşağıdaki gibidir:

1. Merhaba uygulama arka ucu:
   * Arka uç veritabanı güvenli yükünde depolar.
   * Merhaba (güvenli hiçbir bilgi gönderilmez) Bu bildirim toohello Android bir aygıtın Kimliğini gönderir.
2. Merhaba cihaza hello bildirim alırken Hello uygulamanın:
   * Merhaba Android cihaz hello arka uç isteyen hello güvenli yükü bağlanır.
   * Merhaba uygulama hello yükü hello aygıt bildirim olarak gösterebilir.

Merhaba kullanıcı oturum açtığında sonra akışı önceki hello (ve Bu öğreticide), biz hello aygıt varsayın toonote kimlik doğrulama belirtecini yerel depolama biriminde, depolar. önemlidir. Merhaba aygıt hello bildirim'ın güvenli yükü bu belirteci kullanarak alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır. Uygulamanızın kimlik doğrulama belirteçleri hello aygıtta depolamaz veya bu belirteçleri süresi, hello anında iletme bildirimi aldığında gerçekleştireceği hello cihaz uygulaması hello kullanıcı toolaunch hello uygulama isteyen genel bir bildirim görüntülemelidir. Merhaba uygulama hello kullanıcının kimliğini doğrular ve hello bildirim yükü gösterir.

Bu öğretici nasıl toosend güvenli anında iletme bildirimleri gösterir. Merhaba üzerinde derlemeler [kullanıcılara bildirme](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) henüz yapmadıysanız, hello adımları Bu öğreticinin ilk tamamlamanız gerekir böylece öğretici.

> [!NOTE]
> Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Merhaba Android projesi değiştirme
Uygulama arka uç toosend yalnızca hello değiştiren göre *kimliği* bir anında iletme bildirimi bildirim ve geri arama, arka uç tooretrieve hello görüntülenen ileti toobe güvenli, Android uygulaması toohandle toochange sahip.
tooachieve bu hedefe toomake Android uygulamanızı bilir emin sahip nasıl tooauthenticate kendisi, hello anında iletme bildirimleri aldığında uç ile.

Biz şimdi hello değiştirecek *oturum açma* sipariş toosave hello kimlik doğrulaması üstbilgi değeri hello akışında paylaşılan tercihleri, uygulamanızın. Benzer mekanizmaları kullanılan toostore olabilir kullanıcı kimlik bilgilerini gerek kalmadan toouse uygulama hello tüm kimlik doğrulama belirteci (örneğin OAuth belirteçlerini) sahip olacaktır.

1. Merhaba hello üstündeki sabitleri aşağıdaki hello Android uygulaması projenize eklemek **MainActivity** sınıfı:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Merhaba yine de **MainActivity** sınıfı, güncelleştirme hello `getAuthorizationHeader()` koddan yöntemi toocontain hello:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Merhaba aşağıdakileri ekleyin `import` deyimleri hello hello üstündeki **MainActivity** dosyası:
   
        import android.content.SharedPreferences;

Şimdi biz hello bildirim alındığında çağrılan hello işleyici değiştireceksiniz.

1. Merhaba, **MyHandler** sınıfı değiştirmek hello `OnReceive()` yöntemi toocontain:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Merhaba eklemek `retrieveNotification()` hello yer tutucu değiştirme yöntemi `{back-end endpoint}` , arka uç dağıtırken elde hello arka uç uç noktası ile:
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

Bu yöntem, uygulama arka uç tooretrieve hello bildirim hello depolanan hello kimlik bilgilerini kullanarak ve paylaşılan tercihleri normal bir bildirim görüntüler içerik çağırır. Merhaba bildirim toohello uygulama kullanıcı herhangi bir anında iletme bildirimi gibi tam olarak arar.

Tercih toohandle hello örneklerini eksik kimlik doğrulama üstbilgisi özelliği ya da reddetme hello arka uç tarafından olduğuna dikkat edin. Bu durumlarda belirli işleme Hello çoğunlukla, hedef kullanıcı deneyimi bağlıdır. Toodisplay hello kullanıcı tooauthenticate tooretrieve hello gerçek bildirimi için genel bir istem içeren bir bildirim bir seçenektir.

## <a name="run-hello-application"></a>Merhaba uygulama çalıştırın
toorun Merhaba uygulama, aşağıdaki hello:

1. Emin olun **AppBackend** Azure'da dağıtılır. Visual Studio kullanıyorsanız hello çalıştırın **AppBackend** Web API uygulaması. Bir ASP.NET web sayfası görüntülenir.
2. Eclipse'te, Android fiziksel bir aygıt veya hello öykünücüsü hello uygulamayı çalıştırın.
3. Hello Android uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin. Bunlar herhangi bir dize olabilir, ancak bunlar olmalıdır hello aynı değeri.
4. Merhaba Android uygulamanın kullanıcı Arabirimi, tıklayın **oturum**. Ardından **Gönder itme**.

