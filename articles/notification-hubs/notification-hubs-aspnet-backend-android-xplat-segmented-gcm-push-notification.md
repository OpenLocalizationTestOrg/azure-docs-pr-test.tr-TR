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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="926ef-103">Bildirim hub'ları toosend son dakika haberleri kullanın</span><span class="sxs-lookup"><span data-stu-id="926ef-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="926ef-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="926ef-104">Overview</span></span>
<span data-ttu-id="926ef-105">Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast son dakika haberleri bildirimleri tooan Android uygulaması.</span><span class="sxs-lookup"><span data-stu-id="926ef-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="926ef-106">Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak.</span><span class="sxs-lookup"><span data-stu-id="926ef-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="926ef-107">Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin, RSS Okuyucu, müzik fanlar, vb. için uygulamaları ilgi bildirilen kullanıcıların sahip olduğu bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="926ef-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="926ef-108">Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken.</span><span class="sxs-lookup"><span data-stu-id="926ef-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="926ef-109">Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="926ef-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="926ef-110">Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="926ef-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="926ef-111">Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="926ef-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="926ef-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="926ef-112">Prerequisites</span></span>
<span data-ttu-id="926ef-113">Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="926ef-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="926ef-114">Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="926ef-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="926ef-115">Kategori seçimi toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="926ef-115">Add category selection toohello app</span></span>
<span data-ttu-id="926ef-116">Merhaba ilk tooadd hello hello kullanıcı tooselect kategorileri tooregister etkinleştiren kullanıcı Arabirimi öğeleri tooyour varolan ana etkinlik adımdır.</span><span class="sxs-lookup"><span data-stu-id="926ef-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="926ef-117">bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır.</span><span class="sxs-lookup"><span data-stu-id="926ef-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="926ef-118">Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="926ef-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="926ef-119">Res/layout/activity_main.xml dosyanızı açın ve hello içerikle hello aşağıdakileri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="926ef-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
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
2. <span data-ttu-id="926ef-120">Res/values/strings.xml dosyanızı açın ve hello aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="926ef-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="926ef-121">Main_activity.xml grafik düzeninizi gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="926ef-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="926ef-122">Şimdi bir sınıf oluşturun **bildirimleri** hello aynı olarak paketini, **MainActivity** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="926ef-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
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
   
    <span data-ttu-id="926ef-123">Bu sınıf hello yerel depolama toostore hello kategorilerini bu aygıtta tooreceive olduğunu haber kullanır.</span><span class="sxs-lookup"><span data-stu-id="926ef-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="926ef-124">Ayrıca, bu kategorilerin yöntemleri tooregister içerir.</span><span class="sxs-lookup"><span data-stu-id="926ef-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="926ef-125">İçinde **MainActivity** sınıfı kaldırmak için özel alanlar **NotificationHub** ve **GoogleCloudMessaging**, ve bir alan ekleyin **bildirimleri**:</span><span class="sxs-lookup"><span data-stu-id="926ef-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="926ef-126">Ardından hello **onCreate** yöntemi, hello Kaldır hello başlatılması **hub** alan ve hello **registerWithNotificationHubs** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="926ef-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="926ef-127">Merhaba örneği başlatılamıyor satırlar aşağıdaki hello eklemek **bildirimleri** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="926ef-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="926ef-128">`HubName`ve `HubListenConnectionString` hello ile zaten ayarlanmış `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultListenSharedAccessSignature* elde daha önce.</span><span class="sxs-lookup"><span data-stu-id="926ef-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="926ef-129">Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak.</span><span class="sxs-lookup"><span data-stu-id="926ef-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="926ef-130">Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="926ef-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="926ef-131">Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="926ef-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="926ef-132">Ardından, aşağıdaki hello alır ekleyin ve `subscribe` yöntemi toohandle hello abone düğmesi olay'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="926ef-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="926ef-133">Bu yöntem kategorileri ve kullandığı hello listesini oluşturur **bildirimleri** sınıf toostore hello hello yerel depolama listesinde ve bildirim hub'ınıza hello karşılık gelen etiketleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="926ef-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="926ef-134">Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="926ef-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="926ef-135">Uygulamanızı mümkün toostore kategorileri kümesi hello cihazda yerel depolama sunulmuştur ve kategorisi seçimine hello kullanıcı değişiklikleri hello her hello bildirim hub'ı ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="926ef-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="926ef-136">Bildirimler için kaydolun</span><span class="sxs-lookup"><span data-stu-id="926ef-136">Register for notifications</span></span>
<span data-ttu-id="926ef-137">Yerel depolamada depolanan hello kategorileri kullanarak başlangıçta hello bildirim hub'ı ile adımları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="926ef-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="926ef-138">Google Cloud Messaging (GCM) tarafından atanan hello RegistrationId herhangi bir zamanda değiştiğinden bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="926ef-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="926ef-139">Bu hello uygulama her başlatıldığında bu örnek bir bildirime kaydolur.</span><span class="sxs-lookup"><span data-stu-id="926ef-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="926ef-140">Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="926ef-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="926ef-141">Merhaba hello sonunda koddan hello eklemek **onCreate** hello yönteminde **MainActivity** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="926ef-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="926ef-142">Bu hello uygulama her başlatıldığında hello kategorileri yerel depodan alır ve bu kategorilerin bir kayda istekleri emin olur.</span><span class="sxs-lookup"><span data-stu-id="926ef-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="926ef-143">Merhaba güncelleştirme `onStart()` hello yöntemi `MainActivity` gibi sınıfı:</span><span class="sxs-lookup"><span data-stu-id="926ef-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="926ef-144">@Overridekorumalı void onStart() {</span><span class="sxs-lookup"><span data-stu-id="926ef-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="926ef-145">}</span><span class="sxs-lookup"><span data-stu-id="926ef-145">}</span></span>
   
    <span data-ttu-id="926ef-146">Bu, önceden kaydedilmiş kategorileri hello durumlarına dayalı hello ana etkinlik güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="926ef-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="926ef-147">Merhaba uygulama tamamlanmıştır ve kategorisi seçimine hello kullanıcı değişiklikleri hello her kategori kümesini hello aygıt kullanılan yerel depolama tooregister hello bildirim hub'ı ile depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="926ef-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="926ef-148">Ardından, biz kategori bildirimleri toothis uygulamanın gönderebileceği bir arka uç tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="926ef-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="926ef-149">Etiketli bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="926ef-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="926ef-150">Merhaba uygulamayı çalıştırın ve bildirimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="926ef-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="926ef-151">Android Studio'da hello uygulaması oluşturma ve bir cihaz veya öykünücü başlatın.</span><span class="sxs-lookup"><span data-stu-id="926ef-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="926ef-152">Bir dizi kullanıcı Arabirimi sağlar bu hello uygulama değiştirir Not hello kategorileri toosubscribe seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="926ef-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="926ef-153">Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.</span><span class="sxs-lookup"><span data-stu-id="926ef-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="926ef-154">Merhaba uygulama seçili hello kategoriler etiketleri dönüştürür ve seçili hello etiketleri için yeni bir cihaz kaydı hello bildirim hub'ından ister.</span><span class="sxs-lookup"><span data-stu-id="926ef-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="926ef-155">Merhaba kayıtlı kategorileri döndürülen ve bir bildirim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="926ef-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="926ef-156">Merhaba .NET konsol uygulaması çalıştırarak yeni bir bildirim gönderin.</span><span class="sxs-lookup"><span data-stu-id="926ef-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="926ef-157">Alternatif olarak, bildirim hub'ınızın hello hata ayıklama sekmesini hello kullanarak etiketli şablon bildirimleri gönderebilir [Klasik Azure portalı].</span><span class="sxs-lookup"><span data-stu-id="926ef-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="926ef-158">Seçili hello kategorileri için bildirimler bildirimleri görünür.</span><span class="sxs-lookup"><span data-stu-id="926ef-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="926ef-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="926ef-159">Next steps</span></span>
<span data-ttu-id="926ef-160">Biz bu öğreticide öğrenilen nasıl kategoriye göre son dakika haberleri toobroadcast.</span><span class="sxs-lookup"><span data-stu-id="926ef-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="926ef-161">Diğer gelişmiş Notification Hubs senaryoları vurgulayın öğreticileri aşağıdaki hello birini Tamamlanıyor göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="926ef-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="926ef-162">[Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]</span><span class="sxs-lookup"><span data-stu-id="926ef-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="926ef-163">Haber uygulama tooenable göndermek çiğnemekten tooexpand hello bildirimleri nasıl yerelleştirilmiş öğrenin.</span><span class="sxs-lookup"><span data-stu-id="926ef-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
