---
title: "aaaNotification hub haber Öğreticisi çiğnemekten - Android"
description: "Bilgi nasıl toouse Azure hizmet veri yolu bildirim hub'ları toosend haber bildirimleri tooAndroid aygıtları kesiliyor."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Bildirim hub'ları toosend son dakika haberleri kullanın
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast son dakika haberleri bildirimleri tooan Android uygulaması. Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak. Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin, RSS Okuyucu, müzik fanlar, vb. için uygulamaları ilgi bildirilen kullanıcıların sahip olduğu bir senaryodur.

Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken. Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız. Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez. Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Ön koşullar
Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started]. Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].

## <a name="add-category-selection-toohello-app"></a>Kategori seçimi toohello uygulama Ekle
Merhaba ilk tooadd hello hello kullanıcı tooselect kategorileri tooregister etkinleştiren kullanıcı Arabirimi öğeleri tooyour varolan ana etkinlik adımdır. bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır. Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.

1. Res/layout/activity_main.xml dosyanızı açın ve hello içerikle hello aşağıdakileri değiştirin:
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. Res/values/strings.xml dosyanızı açın ve hello aşağıdaki satırları ekleyin:
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    Main_activity.xml grafik düzeninizi gibi görünmelidir:
   
    ![][A1]
3. Şimdi bir sınıf oluşturun **bildirimleri** hello aynı olarak paketini, **MainActivity** sınıfı.
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    Bu sınıf hello yerel depolama toostore hello kategorilerini bu aygıtta tooreceive olduğunu haber kullanır. Ayrıca, bu kategorilerin yöntemleri tooregister içerir.
4. İçinde **MainActivity** sınıfı kaldırmak için özel alanlar **NotificationHub** ve **GoogleCloudMessaging**, ve bir alan ekleyin **bildirimleri**:
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. Ardından hello **onCreate** yöntemi, hello Kaldır hello başlatılması **hub** alan ve hello **registerWithNotificationHubs** yöntemi. Merhaba örneği başlatılamıyor satırlar aşağıdaki hello eklemek **bildirimleri** sınıfı. 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`ve `HubListenConnectionString` hello ile zaten ayarlanmış `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultListenSharedAccessSignature* elde daha önce.

    > [AZURE.NOTE] Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak. Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor. Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.


1. Ardından, aşağıdaki hello alır ekleyin ve `subscribe` yöntemi toohandle hello abone düğmesi olay'ı tıklatın:
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    Bu yöntem kategorileri ve kullandığı hello listesini oluşturur **bildirimleri** sınıf toostore hello hello yerel depolama listesinde ve bildirim hub'ınıza hello karşılık gelen etiketleri kaydedin. Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.

Uygulamanızı mümkün toostore kategorileri kümesi hello cihazda yerel depolama sunulmuştur ve kategorisi seçimine hello kullanıcı değişiklikleri hello her hello bildirim hub'ı ile kaydedin.

## <a name="register-for-notifications"></a>Bildirimler için kaydolun
Yerel depolamada depolanan hello kategorileri kullanarak başlangıçta hello bildirim hub'ı ile adımları kaydedin.

> [!NOTE]
> Google Cloud Messaging (GCM) tarafından atanan hello RegistrationId herhangi bir zamanda değiştiğinden bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz. Bu hello uygulama her başlatıldığında bu örnek bir bildirime kaydolur. Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.
> 
> 

1. Merhaba hello sonunda koddan hello eklemek **onCreate** hello yönteminde **MainActivity** sınıfı:
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    Bu hello uygulama her başlatıldığında hello kategorileri yerel depodan alır ve bu kategorilerin bir kayda istekleri emin olur. 
2. Merhaba güncelleştirme `onStart()` hello yöntemi `MainActivity` gibi sınıfı:
   
    @Overridekorumalı void onStart() {
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    }
   
    Bu, önceden kaydedilmiş kategorileri hello durumlarına dayalı hello ana etkinlik güncelleştirir.

Merhaba uygulama tamamlanmıştır ve kategorisi seçimine hello kullanıcı değişiklikleri hello her kategori kümesini hello aygıt kullanılan yerel depolama tooregister hello bildirim hub'ı ile depolayabilirsiniz. Ardından, biz kategori bildirimleri toothis uygulamanın gönderebileceği bir arka uç tanımlayacaksınız.

## <a name="sending-tagged-notifications"></a>Etiketli bildirimleri gönderme
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Merhaba uygulamayı çalıştırın ve bildirimler oluşturma
1. Android Studio'da hello uygulaması oluşturma ve bir cihaz veya öykünücü başlatın.
   
    Bir dizi kullanıcı Arabirimi sağlar bu hello uygulama değiştirir Not hello kategorileri toosubscribe seçmenize olanak sağlar.
2. Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.
   
    Merhaba uygulama seçili hello kategoriler etiketleri dönüştürür ve seçili hello etiketleri için yeni bir cihaz kaydı hello bildirim hub'ından ister. Merhaba kayıtlı kategorileri döndürülen ve bir bildirim görüntülenir.
3. Merhaba .NET konsol uygulaması çalıştırarak yeni bir bildirim gönderin.  Alternatif olarak, bildirim hub'ınızın hello hata ayıklama sekmesini hello kullanarak etiketli şablon bildirimleri gönderebilir [Klasik Azure portalı].
   
    Seçili hello kategorileri için bildirimler bildirimleri görünür.

## <a name="next-steps"></a>Sonraki adımlar
Biz bu öğreticide öğrenilen nasıl kategoriye göre son dakika haberleri toobroadcast. Diğer gelişmiş Notification Hubs senaryoları vurgulayın öğreticileri aşağıdaki hello birini Tamamlanıyor göz önünde bulundurun:

* [Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]
  
    Haber uygulama tooenable göndermek çiğnemekten tooexpand hello bildirimleri nasıl yerelleştirilmiş öğrenin.

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Klasik Azure portalı]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
