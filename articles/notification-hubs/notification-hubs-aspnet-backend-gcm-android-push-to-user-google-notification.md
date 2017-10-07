---
title: ".NET arka ucu ile aaaAzure Notification Hubs kullanıcılara bildirme Android için"
description: "Nasıl toosend anında iletme bildirimleri toousers Azure'da öğrenin. Android için Java dilinde yazılan kod örnekleri"
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: b042d2e6fb7f7c861c378526a8a0d59ab75beef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a>Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile Android için
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Genel Bakış
Azure'da anında iletme bildirimi destek tooaccess kullanımı kolay, multiplatform ve Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir ölçeklendirilmiş gönderim altyapısı sağlar Platform. Bu öğretici nasıl toouse Azure Notification Hubs toosend anında iletme bildirimleri tooa belirli uygulama kullanıcısı belirli bir cihazda gösterir. Bir ASP.NET Webapı arka kullanılan tooauthenticate istemcileri ve toogenerate bildirimleri hello Kılavuzu konusundaki gösterildiği gibidir [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend). Hello oluşturulan hello bildirim hub'ında Bu öğretici derlemeler [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md) Öğreticisi.

> [!NOTE]
> Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a>Merhaba Android projesi oluşturma
Merhaba sonraki toocreate Merhaba Android uygulaması adımdır.

1. Merhaba izleyin [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md) öğretici toocreate ve GCM, uygulama tooreceive anında iletme bildirimleri yapılandırabilirsiniz.
2. Açık, **res/layout/activity_main.xml** dosya, hello içerik tanımları aşağıdaki hello ile değiştirin.
   
    Bu, bir kullanıcı olarak oturum açmayı yeni EDITTEXT denetimlerini ekler. Ayrıca bir alan için gönderdiğiniz bildirimleri parçası olacak bir kullanıcı adı etiketi eklenir:
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. Açık, **res/values/strings.xml** dosya ve hello yerine `send_button` hello aşağıdaki tanımıyla satırları hello için bu yeniden tanımla hello dizesi `send_button` ve diğer denetimlerin hello için dizeleri ekleyin:
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    Main_activity.xml grafik düzeninizi gibi görünmelidir:
   
    ![][A1]
4. Adlı yeni bir sınıf oluşturun **RegisterClient** hello aynı olarak paketini, `MainActivity` sınıfı. Merhaba kodunu aşağıda hello yeni sınıf dosyası için kullanın.
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    Bu bileşen hello REST çağrılarını gerekli toocontact hello uygulama arka ucu, anında iletme bildirimleri için sipariş tooregister içinde uygular. Merhaba da yerel olarak depoladığı *registrationIds* bildirim hub'ı ayrıntılı biçimde açıklandığı gibi hello tarafından oluşturulan [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend). Merhaba tıklattığınızda yerel depolamada depolanan bir yetki belirteci kullandığına dikkat edin **oturum** düğmesi.
5. İçinde `MainActivity` sınıfı kaldırın veya yorum yapmak için özel alan çıkışı `NotificationHub`, ve hello için bir alan ekleyin `RegisterClient` sınıfı ve ASP.NET ucun uç noktası için bir dize. Emin tooreplace olması `<Enter Your Backend Endpoint>` hello ile gerçek arka uç noktanızı elde daha önce. Örneğin, `http://mybackend.azurewebsites.net`.

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. İçinde `MainActivity` sınıfında hello `onCreate` yöntemi, kaldırmak veya açıklama hello hello başlatma `hub` alan ve hello çağrısı toohello `registerWithNotificationHubs` yöntemi. Kod tooinitialize hello örneği eklemek `RegisterClient` sınıfı. Merhaba yöntemi izleyerek hello içermelidir:
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. İçinde `MainActivity` sınıfı, silmek veya yorum hello tüm `registerWithNotificationHubs` yöntemi. Bu öğreticide kullanılmayacak.
3. Merhaba aşağıdakileri ekleyin `import` deyimleri tooyour **MainActivity.java** dosya.
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. Ardından, aşağıdaki yöntemleri toohandle hello hello ekleyin **oturum** olay ve anında iletme bildirimleri gönderme düğmesini tıklatın.
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed tooregister", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls hello ASP.NET WebAPI backend toosend hello notification message
         * toohello platform notification service based on hello pns parameter.
         *
         * @param pns     hello platform notification service toosend hello notification message to. Must
         *                be one of hello following ("wns", "gcm", "apns").
         * @param userTag hello tag for hello user who will receive hello notification message. This string
         *                must not contain spaces or special characters.
         * @param message hello notification message string. This string must include hello double quotes
         *                toobe used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed toosend " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    Merhaba `login` hello için işleyici **oturum** düğmesi oluşturur temel kimlik doğrulaması belirteci hello giriş kullanıcı adı ve parolasına (Bu, kimlik doğrulama şemasını kullanan herhangi bir belirteci temsil ettiğini unutmayın) kullanarak bir sonra kullanan`RegisterClient`toocall hello arka uç kaydı için.

    Merhaba `sendPush` yöntemi güvenli bildirim toohello kullanıcı hello kullanıcı etiketinde tabanlı hello arka uç tootrigger çağırır. Merhaba platform bildirim hizmetinin `sendPush` hedeflediği bağlıdır hello üzerinde `pns` dizesi geçirilen.

1. İçinde `MainActivity` sınıfı, güncelleştirme hello `sendNotificationButtonOnClick` yöntemi toocall hello `sendPush` hello kullanıcının yöntemiyle seçili platform Bildirim Hizmetleri gibi.
   
       /**
        * Send Notification button click handler. This method sends hello push notification
        * message tooeach platform selected.
        *
        * @param v hello view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-hello-application"></a>Merhaba uygulama çalıştırın
1. Merhaba uygulaması bir aygıt veya Android Studio kullanarak bir öykünücü çalıştırın.
2. Merhaba Android uygulamada bir kullanıcı adı ve parola girin. Hem de hello olmalıdır aynı dize değeri ve bunlar içermemelidir boşluk veya özel karakter.
3. Merhaba Android uygulamada tıklatın **oturum**. Bildiren bir bildirim iletisi için bekleyin **günlüğe giriş ve kayıtlı**. Bu hello etkinleştirecek **bildirim gönder** düğmesi.
   
    ![][A2]
4. Merhaba iki durumlu düğmeler tooenable tıklatın sahip olduğu tüm platformlar hello uygulaması çalıştıran ve bir kullanıcının kayıtlı.
5. Merhaba bildirim iletisi alırsınız hello kullanıcının adını girin. Bu kullanıcı bildirimleri hello hedef cihazlarda kayıtlı olması gerekir.
6. Bir ileti için hello kullanıcı tooreceive anında bildirim iletisi girin.
7. Tıklatın **bildirim gönder**.  Merhaba eşleşen bir kullanıcı adı etiketi ile bir kaydı var her bir cihaz hello anında iletme bildirimi alırsınız.

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
