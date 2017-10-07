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
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="18f07-104">Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile Android için</span><span class="sxs-lookup"><span data-stu-id="18f07-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="18f07-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="18f07-105">Overview</span></span>
<span data-ttu-id="18f07-106">Azure'da anında iletme bildirimi destek tooaccess kullanımı kolay, multiplatform ve Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir ölçeklendirilmiş gönderim altyapısı sağlar Platform.</span><span class="sxs-lookup"><span data-stu-id="18f07-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="18f07-107">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında iletme bildirimleri tooa belirli uygulama kullanıcısı belirli bir cihazda gösterir.</span><span class="sxs-lookup"><span data-stu-id="18f07-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="18f07-108">Bir ASP.NET Webapı arka kullanılan tooauthenticate istemcileri ve toogenerate bildirimleri hello Kılavuzu konusundaki gösterildiği gibidir [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="18f07-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="18f07-109">Hello oluşturulan hello bildirim hub'ında Bu öğretici derlemeler [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="18f07-109">This tutorial builds on hello notification hub that you created in hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="18f07-110">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="18f07-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a><span data-ttu-id="18f07-111">Merhaba Android projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="18f07-111">Create hello Android Project</span></span>
<span data-ttu-id="18f07-112">Merhaba sonraki toocreate Merhaba Android uygulaması adımdır.</span><span class="sxs-lookup"><span data-stu-id="18f07-112">hello next step is toocreate hello Android application.</span></span>

1. <span data-ttu-id="18f07-113">Merhaba izleyin [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md) öğretici toocreate ve GCM, uygulama tooreceive anında iletme bildirimleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18f07-113">Follow hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial toocreate and configure your app tooreceive push notifications from GCM.</span></span>
2. <span data-ttu-id="18f07-114">Açık, **res/layout/activity_main.xml** dosya, hello içerik tanımları aşağıdaki hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="18f07-114">Open your **res/layout/activity_main.xml** file, replace hello with hello following content definitions.</span></span>
   
    <span data-ttu-id="18f07-115">Bu, bir kullanıcı olarak oturum açmayı yeni EDITTEXT denetimlerini ekler.</span><span class="sxs-lookup"><span data-stu-id="18f07-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="18f07-116">Ayrıca bir alan için gönderdiğiniz bildirimleri parçası olacak bir kullanıcı adı etiketi eklenir:</span><span class="sxs-lookup"><span data-stu-id="18f07-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
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
3. <span data-ttu-id="18f07-117">Açık, **res/values/strings.xml** dosya ve hello yerine `send_button` hello aşağıdaki tanımıyla satırları hello için bu yeniden tanımla hello dizesi `send_button` ve diğer denetimlerin hello için dizeleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="18f07-117">Open your **res/values/strings.xml** file and replace hello `send_button` definition with hello following lines that redefine hello string for hello `send_button` and add strings for hello other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="18f07-118">Main_activity.xml grafik düzeninizi gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="18f07-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="18f07-119">Adlı yeni bir sınıf oluşturun **RegisterClient** hello aynı olarak paketini, `MainActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="18f07-119">Create a new class named **RegisterClient** in hello same package as your `MainActivity` class.</span></span> <span data-ttu-id="18f07-120">Merhaba kodunu aşağıda hello yeni sınıf dosyası için kullanın.</span><span class="sxs-lookup"><span data-stu-id="18f07-120">Use hello code below for hello new class file.</span></span>
   
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
   
    <span data-ttu-id="18f07-121">Bu bileşen hello REST çağrılarını gerekli toocontact hello uygulama arka ucu, anında iletme bildirimleri için sipariş tooregister içinde uygular.</span><span class="sxs-lookup"><span data-stu-id="18f07-121">This component implements hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="18f07-122">Merhaba da yerel olarak depoladığı *registrationIds* bildirim hub'ı ayrıntılı biçimde açıklandığı gibi hello tarafından oluşturulan [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="18f07-122">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="18f07-123">Merhaba tıklattığınızda yerel depolamada depolanan bir yetki belirteci kullandığına dikkat edin **oturum** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18f07-123">Note that it uses an authorization token stored in local storage when you click hello **Log in** button.</span></span>
5. <span data-ttu-id="18f07-124">İçinde `MainActivity` sınıfı kaldırın veya yorum yapmak için özel alan çıkışı `NotificationHub`, ve hello için bir alan ekleyin `RegisterClient` sınıfı ve ASP.NET ucun uç noktası için bir dize.</span><span class="sxs-lookup"><span data-stu-id="18f07-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for hello `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="18f07-125">Emin tooreplace olması `<Enter Your Backend Endpoint>` hello ile gerçek arka uç noktanızı elde daha önce.</span><span class="sxs-lookup"><span data-stu-id="18f07-125">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="18f07-126">Örneğin, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="18f07-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="18f07-127">İçinde `MainActivity` sınıfında hello `onCreate` yöntemi, kaldırmak veya açıklama hello hello başlatma `hub` alan ve hello çağrısı toohello `registerWithNotificationHubs` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="18f07-127">In your `MainActivity` class, in hello `onCreate` method, remove or comment out hello initialization of hello `hub` field and hello call toohello `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="18f07-128">Kod tooinitialize hello örneği eklemek `RegisterClient` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="18f07-128">Then add code tooinitialize an instance of hello `RegisterClient` class.</span></span> <span data-ttu-id="18f07-129">Merhaba yöntemi izleyerek hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="18f07-129">hello method should contain hello following lines:</span></span>
   
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
2. <span data-ttu-id="18f07-130">İçinde `MainActivity` sınıfı, silmek veya yorum hello tüm `registerWithNotificationHubs` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="18f07-130">In your `MainActivity` class, delete or comment out hello entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="18f07-131">Bu öğreticide kullanılmayacak.</span><span class="sxs-lookup"><span data-stu-id="18f07-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="18f07-132">Merhaba aşağıdakileri ekleyin `import` deyimleri tooyour **MainActivity.java** dosya.</span><span class="sxs-lookup"><span data-stu-id="18f07-132">Add hello following `import` statements tooyour **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="18f07-133">Ardından, aşağıdaki yöntemleri toohandle hello hello ekleyin **oturum** olay ve anında iletme bildirimleri gönderme düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="18f07-133">Then, add hello following methods toohandle hello **Log in** button click event and sending push notifications.</span></span>
   
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

    <span data-ttu-id="18f07-134">Merhaba `login` hello için işleyici **oturum** düğmesi oluşturur temel kimlik doğrulaması belirteci hello giriş kullanıcı adı ve parolasına (Bu, kimlik doğrulama şemasını kullanan herhangi bir belirteci temsil ettiğini unutmayın) kullanarak bir sonra kullanan`RegisterClient`toocall hello arka uç kaydı için.</span><span class="sxs-lookup"><span data-stu-id="18f07-134">hello `login` handler for hello **Log in** button generates a basic authentication token using on hello input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` toocall hello backend for registration.</span></span>

    <span data-ttu-id="18f07-135">Merhaba `sendPush` yöntemi güvenli bildirim toohello kullanıcı hello kullanıcı etiketinde tabanlı hello arka uç tootrigger çağırır.</span><span class="sxs-lookup"><span data-stu-id="18f07-135">hello `sendPush` method calls hello backend tootrigger a secure notification toohello user based on hello user tag.</span></span> <span data-ttu-id="18f07-136">Merhaba platform bildirim hizmetinin `sendPush` hedeflediği bağlıdır hello üzerinde `pns` dizesi geçirilen.</span><span class="sxs-lookup"><span data-stu-id="18f07-136">hello platform notification service that `sendPush` targets depends on hello `pns` string passed in.</span></span>

1. <span data-ttu-id="18f07-137">İçinde `MainActivity` sınıfı, güncelleştirme hello `sendNotificationButtonOnClick` yöntemi toocall hello `sendPush` hello kullanıcının yöntemiyle seçili platform Bildirim Hizmetleri gibi.</span><span class="sxs-lookup"><span data-stu-id="18f07-137">In your `MainActivity` class, update hello `sendNotificationButtonOnClick` method toocall hello `sendPush` method with hello user's selected platform notification services as follows.</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="18f07-138">Merhaba uygulama çalıştırın</span><span class="sxs-lookup"><span data-stu-id="18f07-138">Run hello Application</span></span>
1. <span data-ttu-id="18f07-139">Merhaba uygulaması bir aygıt veya Android Studio kullanarak bir öykünücü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="18f07-139">Run hello application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="18f07-140">Merhaba Android uygulamada bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="18f07-140">In hello Android app, enter a username and password.</span></span> <span data-ttu-id="18f07-141">Hem de hello olmalıdır aynı dize değeri ve bunlar içermemelidir boşluk veya özel karakter.</span><span class="sxs-lookup"><span data-stu-id="18f07-141">They must both be hello same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="18f07-142">Merhaba Android uygulamada tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="18f07-142">In hello Android app, click **Log in**.</span></span> <span data-ttu-id="18f07-143">Bildiren bir bildirim iletisi için bekleyin **günlüğe giriş ve kayıtlı**.</span><span class="sxs-lookup"><span data-stu-id="18f07-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="18f07-144">Bu hello etkinleştirecek **bildirim gönder** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18f07-144">This will enable hello **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="18f07-145">Merhaba iki durumlu düğmeler tooenable tıklatın sahip olduğu tüm platformlar hello uygulaması çalıştıran ve bir kullanıcının kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="18f07-145">Click hello toggle buttons tooenable all platforms where you have ran hello app and registered a user.</span></span>
5. <span data-ttu-id="18f07-146">Merhaba bildirim iletisi alırsınız hello kullanıcının adını girin.</span><span class="sxs-lookup"><span data-stu-id="18f07-146">Enter hello user's name that will receive hello notification message.</span></span> <span data-ttu-id="18f07-147">Bu kullanıcı bildirimleri hello hedef cihazlarda kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="18f07-147">That user must be registered for notifications on hello target devices.</span></span>
6. <span data-ttu-id="18f07-148">Bir ileti için hello kullanıcı tooreceive anında bildirim iletisi girin.</span><span class="sxs-lookup"><span data-stu-id="18f07-148">Enter a message for hello user tooreceive as a push notification message.</span></span>
7. <span data-ttu-id="18f07-149">Tıklatın **bildirim gönder**.</span><span class="sxs-lookup"><span data-stu-id="18f07-149">Click **Send Notification**.</span></span>  <span data-ttu-id="18f07-150">Merhaba eşleşen bir kullanıcı adı etiketi ile bir kaydı var her bir cihaz hello anında iletme bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="18f07-150">Each device that has a registration with hello matching username tag will receive hello push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
