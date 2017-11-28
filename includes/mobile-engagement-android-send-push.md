
### <a name="update-manifest-file-to-enable-notifications"></a><span data-ttu-id="b61b1-101">Bildirimleri etkinleştirmek için bildirim dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b61b1-101">Update manifest file to enable notifications</span></span>
<span data-ttu-id="b61b1-102">Aşağıdaki uygulama içi mesajlaşma kaynaklarını aşağıdaki Manifest.xml dosyasında `<application>` ve `</application>` etiketleri arasına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b61b1-102">Copy the in-app messaging resources below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="b61b1-103">Bildirimler için simge belirtme</span><span class="sxs-lookup"><span data-stu-id="b61b1-103">Specify an icon for notifications</span></span>
<span data-ttu-id="b61b1-104">Manifest.xml dosyanızda yer alan aşağıdaki XML parçacığını `<application>` ve `</application>` etiketleri arasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b61b1-104">Paste the following XML snippet in your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="b61b1-105">Böylece simgenin hem sistemde, hem de uygulama içi bildirimlerde görüntüleneceği belirtilir.</span><span class="sxs-lookup"><span data-stu-id="b61b1-105">This defines the icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="b61b1-106">Bu, uygulama içi bildirimler için isteğe bağlı olsa da, sistem bildirimleri için zorunludur.</span><span class="sxs-lookup"><span data-stu-id="b61b1-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="b61b1-107">Android, geçersiz simgelere sahip sistem bildirimlerini reddeder.</span><span class="sxs-lookup"><span data-stu-id="b61b1-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="b61b1-108">**drawable** klasörlerinden birinde bulunan simgeleri kullandığınızdan emin olun (örneğin, ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="b61b1-108">Make sure you are using an icon that exists in one of the **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="b61b1-109">**mipmap** klasörü desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="b61b1-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="b61b1-110">**Başlatıcı** simgesi kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="b61b1-110">You should not use the **launcher** icon.</span></span> <span data-ttu-id="b61b1-111">Bunun farklı bir çözünürlüğü vardır ve çoğunlukla desteklemediğimiz mipmap klasörlerinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="b61b1-111">It has a different resolution and is usually in the mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="b61b1-112">Gerçek uygulamalar için, her[Android tasarım yönergesi](http://developer.android.com/design/patterns/notifications.html) için bir bildirime uygun simgeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b61b1-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="b61b1-113">Doğru simge çözünürlüğü kullandığınızdan emin olmak için [bu örneklere](https://www.google.com/design/icons) bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b61b1-113">To be sure to use correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="b61b1-114">Kayarak **Bildirim** bölümüne gidin, simgeye tıklayın ve ardından simge çizilebilir kümesini indirmek için `PNGS` öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b61b1-114">Scroll down to the **Notification** section, click an icon, and then click `PNGS` to download the icon drawable set.</span></span> <span data-ttu-id="b61b1-115">Simgenin her sürümü için hangi drawable klasörlerde hangi çözünürlüğün kullanıldığını da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b61b1-115">You can see what drawable folders with which resolution to use for each version of the icon.</span></span>
> 
> 

### <a name="enable-your-app-to-receive-gcm-push-notifications"></a><span data-ttu-id="b61b1-116">GCM anında iletme bildirimlerini almak için uygulamanızı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b61b1-116">Enable your app to receive GCM push notifications</span></span>
1. <span data-ttu-id="b61b1-117">Firebase proje konsolunuzdan alınan **Gönderen Kimliği**’ni değiştirdikten sonra aşağıdaki kodu, Manifest.xml dosyanızda `<application>` ve `</application>` etiketleri arasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b61b1-117">Paste the following into your Manifest.xml between the `<application>` and `</application>` tags after replacing the **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="b61b1-118">\n kasıtlı olarak konmuştur; bu nedenle proje numarasını bununla bitirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b61b1-118">The \n is intentional so make sure that you end the project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="b61b1-119">Aşağıdaki kodu Manifest.xml dosyanızda `<application>` ve `</application>` etiketleri arasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b61b1-119">Paste the code below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span> <span data-ttu-id="b61b1-120"><Your package name> paket adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b61b1-120">Replace the package name <Your package name>.</span></span>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. <span data-ttu-id="b61b1-121">`<application>` etiketinin önünde vurgulanan son izin kümesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b61b1-121">Add the last set of permissions that are highlighted before the `<application>` tag.</span></span> <span data-ttu-id="b61b1-122">`<Your package name>` öğesini uygulamanızın asıl paket adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b61b1-122">Replace `<Your package name>` by the actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

