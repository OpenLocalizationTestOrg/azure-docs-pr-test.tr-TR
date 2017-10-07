---
title: "aaaAzure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>TooIntegrate Engagement Reach nasıl Android
> [!IMPORTANT]
> TooIntegrate android'de katılım nasıl belge bu kılavuzu izlemeden önce hello açıklanan hello tümleştirme yordamı izlemeniz gerekir.
> 
> 

## <a name="standard-integration"></a>Standart tümleştirme

Projenizdeki hello SDK ulaşma kaynak dosyalarını kopyalayın:

* Hello Hello dosyaları kopyalamak `res/layout` klasörü teslim hello içine hello SDK ile `res/layout` uygulamanızın klasör.
* Hello Hello dosyaları kopyalamak `res/drawable` klasörü teslim hello içine hello SDK ile `res/drawable` uygulamanızın klasör.

Düzenleme, `AndroidManifest.xml` dosyası:

* Ekle bölümden hello (Merhaba arasında `<application>` ve `</application>` etiketleri):
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* Önyüklemede tıklattınız değil bu izni tooreplay sistem bildirimleri gerekir (Aksi halde diskte tutulur ancak artık görüntülenmeyecek, gerçekten tooinclude bu gerekir).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Kopyalama ve bölümden hello düzenleme bildirimler (hem de uygulama ve sistem olanlar) için kullanılan bir simge belirtin (Merhaba arasında `<application>` ve `</application>` etiketleri):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Bu bölüm **zorunlu** sistem bildirimleri Reach kampanyaları oluştururken kullanmayı planlıyorsanız. Android gösterilen gelen sistem bildirimleri simgeler olmadan engeller. Bu bölümde atlarsanız, son kullanıcılarınıza mümkün tooreceive olmayacak şekilde bunları.
> 
> 

* Büyük resim kullanarak sistem bildirimleri ile Kampanyalar oluşturursanız, aşağıdaki izinleri tooadd hello gerekir (Merhaba sonra `</application>` etiketi) eksikse:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * Android M ve uygulamanızı Android API düzeyi 23 ya da daha hedefleyip hedeflemediği ``WRITE_EXTERNAL_STORAGE`` izni kullanıcı onayı gerektirir. Lütfen okuyun [Bu bölümde](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Ayrıca hello belirtebilirsiniz sistem bildirimleri için Hello cihaz halka ve/veya Titret, kampanya ulaşabilirsiniz. Bunun için toowork, toomake izni aşağıdaki hello bildirildiğinden emin olması (Merhaba sonra `</application>` etiketi):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Bu izin olmadan Android gösterildikten gelen sistem bildirimleri engeller, işaretlediyseniz hello halkası veya hello Titret hello Reach kampanya Yöneticisi'nde seçeneği.

## <a name="native-push"></a>Yerel gönderim
Reach modülünün yapılandırılmış, tooconfigure yerel gönderim toobe mümkün tooreceive hello Kampanyalar hello aygıtta gerekir.

Android iki hizmet destekliyoruz:

* Google Play aygıtları: kullanım [Google Cloud Messaging] aşağıdaki hello tarafından [nasıl tooIntegrate engagement GCM Kılavuzu](mobile-engagement-android-gcm-integrate.md) Kılavuzu.
* Amazon aygıtları: kullanım [Amazon Device Messaging] aşağıdaki hello tarafından [nasıl tooIntegrate engagement ADM Kılavuzu](mobile-engagement-android-adm-integrate.md) Kılavuzu.

Tootarget istiyorsanız, Amazon ve Google Play aygıtlar, kendi olası toohave geliştirme için 1 AndroidManifest.xml/APK içindeki tüm öğeler. Ancak GCM kod bulursanız tooAmazon gönderirken, bunlar uygulamanızı reddedebilir.

Bu durumda birden çok APKs kullanmanız gerekir.

**Hazır tooreceive ve görüntü Kampanyalar ulaşmak şimdi uygulamanızı değil!**

## <a name="how-toohandle-data-push"></a>Nasıl toohandle veri gönderme
### <a name="integration"></a>Tümleştirme
Uygulama toobe mümkün istiyorsanız tooreceive ulaşma veri iter, toocreate bir alt sınıfı olması `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` ve hello başvuru `AndroidManifest.xml` dosyası (Merhaba arasında `<application>` ve/veya `</application>` etiketleri):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

Merhaba geçersiz kılabilirsiniz `onDataPushStringReceived` ve `onDataPushBase64Received` geri aramalar. Örnek aşağıda verilmiştir:

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>Kategori
Merhaba kategori parametresi bir veri gönderme kampanya oluşturduğunuzda isteğe bağlıdır ve toofilter verileri iter sağlar. Veri gönderimleri, farklı türlerde işleme birkaç yayın alıcılar varsa kullanışlıdır veya toopush değişik istiyorsanız, `Base64` veri ve istediğiniz tooidentify bunları ayrıştırma önce kendi türü.

### <a name="callbacks-return-parameter"></a>Geri aramalar dönüş parametresi
Bazı yönergeler tooproperly tanıtıcı hello dönüş parametresi işte `onDataPushStringReceived` ve `onDataPushBase64Received`:

* Bir yayın alıcı döndürmelidir `null` içinde nasıl toohandle veri gönderme bilmiyorsa hello geri çağırma. Yayın Alıcınız hello veri gönderimi veya işlemelidir olup olmadığını hello kategori toodetermine kullanmanız gerekir.
* Merhaba yayın alıcı birini döndürmelidir `true` içinde hello veri gönderimi kabul ederse hello geri çağırma.
* Merhaba yayın alıcı birini döndürmelidir `false` içinde hello veri gönderimi algılar ancak herhangi bir nedenle atar hello geri çağırma. Örneğin, sonuç `false` zaman hello alınan veri geçerli değil.
* Bir alıcı döndürür yayın varsa `true` başka döndürür while `false` hello aynı veri gönderimi, hello davranış tanımsızdır için hiçbir zaman, yapmanız gerekir.

Merhaba dönüş türü yalnızca hello ulaşma istatistikleri için kullanılır:

* `Replied`Merhaba yayın alıcıları birini ya da döndürülürse artırılır `true` veya `false`.
* `Actioned`yalnızca hello birini döndürülen alıcıları yayını olmazsa artırılır `true`.

## <a name="how-toocustomize-campaigns"></a>Nasıl toocustomize Kampanyalar
toocustomize Kampanyalar hello Reach SDK sağlanan hello düzenleri değiştirebilirsiniz.

Merhaba düzenleri kullanılan tüm hello tanımlayıcıları tutmak ve özellikle metin görünümleri ve görüntü görünümleri için bir tanımlayıcı kullanın hello görünüm hello türlerini tutmak gerekir. Bazı görünümler yalnızca kullanılan toohide ya da kendi türü değiştirilemez alanları görüntüleyecek. Sağlanan hello düzenleri toochange hello bir görünüm türünü düşünüyorsanız lütfen hello kaynak kodunu denetleyin.

### <a name="notifications"></a>Bildirimler
Bildirimler iki tür vardır: farklı düzeni dosyaları kullanan sistem ve uygulama içi bildirimler.

#### <a name="system-notifications"></a>Sistem bildirimleri
gereksinim duyduğunuz toouse hello toocustomize sistem bildirimleri **kategorileri**. Çok atlayabilirsiniz[kategorileri](#categories).

#### <a name="in-app-notifications"></a>Uygulama bildirimleri
Varsayılan olarak, bir uygulama bildirimi dinamik olarak eklenen toohello geçerli etkinliği kullanıcı arabirimi teşekkürler toohello Android yöntemi görünümdür `addContentView()`. Bu bildirim bir katmana çağrılır. Uygulamanız herhangi bir düzende, toomodify gerektirmediği için bildirim yer paylaşımları hızlı tümleştirme için mükemmeldir.

bildirim yer paylaşımları hello görünümünü toomodify, yalnızca değiştirebileceğiniz hello dosya `engagement_notification_area.xml` tooyour gerekir.

> [!NOTE]
> Merhaba dosya `engagement_notification_overlay.xml` kullanılan toocreate olan bir bildirim katmana hello olduğu hello dosya içeren `engagement_notification_area.xml`. Ayrıca toosuit özelleştirebilirsiniz gereksinimlerinizi (Merhaba bildirim alanında hello katmana içinde konumlandırma ettirilmesi gibi).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Bir etkinlik düzeni bir parçası olarak bildirim düzeni içerir
Yer paylaşımları hızlı tümleştirme için harika ancak kullanışsız veya özel durumlarda yan etkileri olabilir. Merhaba katmana sistem özel etkinlikler için kolay tooprevent yan etkileri kolaylaştırarak bir etkinlik düzeyde özelleştirilebilir.

Bizim bildirim düzeni tooinclude, varolan düzeni teşekkürler toohello içinde Android karar verebilirsiniz **dahil** deyimi. Merhaba aşağıdaki değiştirilmiş bir örneğidir `ListActivity` düzenini yalnızca içeren bir `ListView`.

**Engagement tümleştirmesi önce:**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Engagement tümleştirmesi sonra:**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

Bu örnekte Hello özgün düzeni bir liste görünümü hello en üst düzey öğe kullanılan bu yana bir üst öğe kapsayıcısı eklediğimiz. Ayrıca eklediğimiz `android:layout_weight="1"` bir liste görünümü aşağıda görünümü toobe mümkün tooadd yapılandırılmış `android:layout_height="fill_parent"`.

Merhaba Engagement Reach SDK hello bildirim düzenini bu etkinlikte bulunan ve bu etkinlik için bir katmana eklemez otomatik olarak algılar.

> [!TIP]
> Uygulamanızda bir ListActivity kullanırsanız, görünür bir Reach katmana, hello liste görünümünde tanımlandığında tooclicked öğeleri artık önler. Bu bilinen bir sorundur. toowork bu soruna geçici, kendi listesi etkinlik düzeni gibi hello önceki örnekteki tooembed hello bildirim düzende öneririz.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Etkinlik başına uygulama bildirimini devre dışı bırakma
Merhaba istemiyorsanız katmana toobe tooyour etkinlik eklendi ve kendi düzende hello bildirim düzeni eklemezseniz, bu etkinlik hello hello katmana devre dışı bırakabilir `AndroidManifest.xml` ekleyerek bir `meta-data` bölüm hello aşağıdakileri ister Örnek:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a>Kategorileri
Düzenleri sağlanan hello değiştirdiğinizde, tüm bildirimlerinizi hello görünümünü değiştirin. Çeşitli hedeflenen toodefine (büyük olasılıkla davranışları) bildirimleri için görünür kategoriler. Bir kategori Reach kampanya oluşturduğunuzda belirtilebilir. Bu belgenin sonraki bölümlerinde açıklanan kategoriler de duyuruları ve yoklamaları, özelleştirmenize olanak tanır olduğunu aklınızda bulundurun.

Merhaba uygulaması başlatıldığında tooregister bildirimlerinizi için bir kategori işleyici, tooadd bir çağrı gerekir.

> [!IMPORTANT]
> Merhaba uyarı hello android: işlem özniteliği hakkında okuyun \<android sdk katılım işlem\> hello içinde nasıl tooIntegrate katılım devam etmeden önce Android konuda.
> 
> 

Merhaba aşağıdaki örneği hello önceki uyarı onaylanır ve bir alt sınıfı kullanma varsayar `EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

Merhaba `MyNotifier` nesne uygulamasıdır hello hello bildirim kategori işleyici. Her iki hello uygulaması olan `EngagementNotifier` arabirimi veya hello varsayılan uygulaması bir alt sınıfı: `EngagementDefaultNotifier`.

Aynı bildirim hello Not birkaç kategorisi işleyebilir, bunları şu şekilde kaydedebilirsiniz:

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

tooreplace hello varsayılan kategori uygulaması, aşağıdaki örneğine hello uygulamanızı gibi kaydedebilirsiniz:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

işleyici kullanılan hello geçerli kategorisi çoğu yöntemleri içinde geçersiz parametre olarak geçirilen `EngagementDefaultNotifier`.

Olarak ya da geçirilir bir `String` parametresi veya dolaylı bir `EngagementReachContent` olan nesne bir `getCategory()` yöntemi.

Üzerinde yöntemleri tanımlayarak hello bildirim oluşturma işlemi çoğunu değiştirebilirsiniz `EngagementDefaultNotifier`, daha gelişmiş özelleştirme eşitleyerek için ücretsiz tootake hello teknik belgeler ve hello kaynak koduna bakın.

##### <a name="in-app-notifications"></a>Uygulama bildirimleri
Belirli bir kategorideki için yalnızca toouse alternatif düzenleri istiyorsanız, bu örnek aşağıdaki hello olduğu gibi uygulayabilirsiniz:

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**Örnek `my_notification_overlay.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Gördüğünüz gibi hello katmana görünüm tanımlayıcısı hello standart bir farklıdır. Her düzeni yer paylaşımları için benzersiz bir tanımlayıcı kullanmak önemlidir.

**Örnek `my_notification_area.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

Gördüğünüz gibi hello bildirim alanı görünüm tanımlayıcısı hello standart bir farklıdır. Her düzeni bildirim alanları için benzersiz bir tanımlayıcı kullanır önemlidir.

Bu basit örnek kategorisinin Merhaba ekranında hello üst kısmında gösterilen uygulama (veya uygulama) bildirim yapar. Merhaba bildirim alanında kendisini kullanılan hello standart tanımlayıcıları değişmemiştir.

Tooredefine hello sahip, toochange istiyorsanız `EngagementDefaultNotifier.prepareInAppArea` yöntemi. Önerilir toolook hello teknik belgeler ve hello kaynak kodunu `EngagementNotifier` ve `EngagementDefaultNotifier` bu Gelişmiş özelleştirme düzeyi istiyorsanız.

##### <a name="system-notifications"></a>Sistem bildirimleri
Genişletme tarafından `EngagementDefaultNotifier`, geçersiz kılabilirsiniz `onNotificationPrepared` hello varsayılan uygulaması tarafından hazırlanan tooalter hello bildirim.

Örneğin:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

Bu örnek hello "devam eden" kategorisi kullanıldığında, devam eden bir olay görüntülenmesini içerik için bir sistem bildirimi yapar.

Toobuild hello istiyorsanız `Notification` nesne baştan geri dönebilirsiniz `false` toohello yöntemi ve çağrı `notify` kendiniz hello `NotificationManager`. Bu durumda, tutmanızı önemli bir `contentIntent`, `deleteIntent` ve bildirim tanımlayıcısı tarafından kullanılan hello `EngagementReachReceiver`.

Bu tür bir uygulama doğru bir örneği burada verilmiştir:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>Yalnızca bildirim duyuruları
Merhaba hello yönetimini tıklayın yalnızca duyuru kılarak özelleştirilebilir bir bildirim `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hazırlanmış toomodify hello `Intent`. Bu yöntemi kullanarak tootune hello bayrakları kolayca sağlar.

Örneğin tooadd hello `SINGLE_TOP` bayrağı:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Bu yöntem, eylem URL'si olmadan duyuru kullanılarak çağrılamaz. böylece arka planda ise, sistem bildirimleri eylemi olmadan URL şimdi hello uygulama başlatma eski katılım kullanıcılar için lütfen unutmayın. Hello hedefi özelleştirirken düşünmelisiniz.

Ayrıca uygulayabilirsiniz `EngagementNotifier.executeNotifAnnouncementAction` sıfırdan.

##### <a name="notification-life-cycle"></a>Bildirim yaşam döngüsü
Merhaba varsayılan kategori kullanırken, bazı yaşam döngüsü yöntemleri üzerinde hello denir `EngagementReachInteractiveContent` nesne tooreport istatistikleri ve güncelleştirme hello kampanya durumu:

* Merhaba bildirim uygulamada görüntülenen ya da hello durum çubuğunda put hello `displayNotification` yöntemi (hangi istatistikleri raporları) çağrılır tarafından `EngagementReachAgent` varsa `handleNotification` döndürür `true`.
* Merhaba bildirim kapatıldığında, hello `exitNotification` yöntemi çağrıldığında, istatistik bildirilir ve sonraki Kampanyalar şimdi işlenebilir.
* Merhaba bildirim tıkladıysanız `actionNotification` olduğu adlı istatistik bildirilir ve ilişkili hello hedefi başlatıldığında.

Uygulamanıza `EngagementNotifier` atlamaların hello varsayılan davranışı, toocall bu yaşam döngüsü yöntemleri başınıza gerekir. Örnek hello hello varsayılan davranışı burada atlanır bazı durumlarda gösterilmiştir:

* Genişletme yok `EngagementDefaultNotifier`, sıfırdan kategori işleme uygulanan örn.
* Sistem bildirimleri için hello geçersiz kılınmış `onNotificationPrepared` ve değiştirdiğiniz `contentIntent` veya `deleteIntent` hello içinde `Notification` nesnesi.
* Uygulama bildirimleri için geçersiz kılınmış `prepareInAppArea`emin toomap olması en az `actionNotification` U.I denetimlerin tooone.

> [!NOTE]
> Varsa `handleNotification` bir özel durum, içerik hello silinir ve `dropContent` olarak adlandırılır. Bu durum istatistiklerine bildirilir ve sonraki Kampanyalar şimdi işlenebilir.
> 
> 

### <a name="announcements-and-polls"></a>Duyuruları ve yoklamaları
#### <a name="layouts"></a>Düzenleri
Merhaba değiştirebileceğiniz `engagement_text_announcement.xml`, `engagement_web_announcement.xml` ve `engagement_poll.xml` toocustomize metin Duyurular, web duyuruları ve yoklamaları dosyaları.

Bu dosyalar hello başlık alanı ve hello düğme alanının için iki ortak düzenleri paylaşır. Merhaba düzeni hello başlık `engagement_content_title.xml` ve kullandığı hello hello arka plan için eponymous drawable dosyası. Merhaba hello eylem ve çıkış düğmeleri için Düzen olan `engagement_button_bar.xml` ve kullandığı hello hello arka plan için eponymous drawable dosyası.

Bir yoklamada soru düzeni hello ve seçimleri birkaç kez hello kullanarak dinamik olarak şişirileceğini `engagement_question.xml` düzeni dosyasını hello sorularınız ve hello `engagement_choice.xml` hello seçimler dosya.

#### <a name="categories"></a>Kategoriler
##### <a name="alternate-layouts"></a>Alternatif düzenleri
Bildirimler gibi hello kampanya kategori duyuruları ve yoklamaları için kullanılan toohave alternatif düzenleri olabilir.

Örneğin, bir metin duyuru için bir kategori toocreate genişletebilirsiniz `EngagementTextAnnouncementActivity` ve hello başvuru `AndroidManifest.xml` dosyası:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Merhaba hedefi hello kategoriye Not filtre kullanılır toomake hello farkı hello varsayılan duyuru etkinlik.

Hello SDK ulaşmak için belirli bir kategorideki hello hedefi sistem tooresolve hello sağ etkinliğini kullanır ve hello çözümlemesi başarısız olursa, geri hello varsayılan kategorisine göre döner.

Tooimplement sahip `MyCustomTextAnnouncementActivity`, yalnızca toochange hello düzeni istediğiniz (ancak aynı tanımlayıcılarını görüntüle hello tutmak varsa), yalnızca toodefine hello sınıfı gibi aşağıdaki örneğine hello gerekir:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

yalnızca metin Duyurular, tooreplace hello varsayılan kategorisini değiştirin `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` , uygulamanız tarafından.

Web duyuruları ve yoklamaları için benzer bir şekilde özelleştirilebilir.

Web duyuruları için genişletebilirsiniz `EngagementWebAnnouncementActivity` ve hello etkinlik bildirmek `AndroidManifest.xml` aşağıdaki örneğine hello ister:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

Anketler için genişletebilirsiniz `EngagementPollActivity` ve içinde hello bildirme `AndroidManifest.xml` aşağıdaki örneğine hello ister:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Sıfırdan uygulama
Hello genişletmeden kategorileri duyuru (ve yoklama) etkinliklerinizi için uygulayabileceğiniz `Engagement*Activity` sınıflar tarafından sağlanan hello Reach SDK. Bu örneğin toodefine görünümlerini aynı hello hello standart düzenleri kullanmaz bir düzen istiyorsanız kullanışlıdır.

Gibi gelişmiş bildirim özelleştirmesi hello kaynak koduna hello standart uygulama toolook önerilir.

Göz önünde bazı şeyleri tookeep şunlardır: ulaşma hello içerik tanıtıcısı olan bir ek parametre hello etkinliği belirli bir amaç (karşılık gelen toohello hedefi Filtresi) ile başlar.

ne zaman hello oluşturma kampanya hello web sitesinde, belirtilen hello alanları içeren tooretrieve hello içerik nesnesini bunu yapabilirsiniz:

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

STATISTICS için hello içerik hello görüntülenen bildirmelisiniz `onResume` olay:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

Ardından, toocall ya da unutmayın `actionContent(this)` veya `exitContent(this)` arka plana hello etkinlik geçmeden önce hello içerik nesne üzerinde.

Ya da yok çağırırsanız `actionContent` veya `exitContent`, istatistikleri (yani hello kampanyası hiçbir analytics) gönderilen olmaz ve daha da önemlisi, hello sonraki kampanyalar, değil hello uygulama işlemini yeniden başlatılana kadar bildirilir.

Yönlendirme veya başka yapılandırma değişiklikleri veya arka plana hello etkinliğine gittiği olup olmadığını hello kod hassas toodetermine olun, standart uygulama yapar emin hello içerik hello kullanıcı hello etkinlik (ya da bırakırsa çıktı olarak bildirilen hello tuşuna basarak `HOME` veya `BACK`) ancak hello yönlendirmesini değişirse değil.

Merhaba ilginç parçası hello şöyledir:

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

Aradığınız varsa, gördüğünüz gibi `actionContent(this)` hello Etkinliğin bitiş sonra `exitContent(this)` herhangi bir etkisi olmadan güvenli bir şekilde çağrılabilir.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
